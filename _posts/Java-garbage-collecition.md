---
title: "Welcome to Jekyll!"
date: 2017-10-20 08:26:28 -0400
categories: jekyll update
---

# Java Garbage Collection

### Stop The World
* GC(Garbage Collection) 을 수행하기 위해 GC 를 수행하는 쓰레드를 제외한 나머지를 모두 멈추는 작업.
* 어떤 GC 를 사용하더라도 STW(Stop The world) 는 발생. 일반적으로 GC 튜닝이란 이 STW 시간을 줄이는 것을 말함.

***
### Garbage Collection
* GC 는 두 가지 가설에 의해 만들어짐.
	1. 대부분의 객체는 금방 접근 불가능 상태(unreachable) 가 됨.
	2. 오래된 객체에서 젊은 객체로의 참조는 아주 적게 존재함.

* 이 가설의 장점을 살리기 위해 크게 2개(세부적으로 3개)로 물리 메모리 공간으로 나눔.
	1. Young Generation : 새로이 생성된 객체가 위치. 대부분의 객체가 금방 접근불가능 상태가 되기때문에 많은 객체가 이 영역에서 생성되었다가 사라짐. 이 영역에서 객체가 사라질 때 Minor GC 라고 지칭함.
	2. Old Generation : 접근 불가능 상태로 되지 않아 Young Generation 에서 살아남은 객체가 복사되는 영역. 대부분 Young Generation 영역보다 크게 할당되며, 크기가 큰 만큼 GC 는 비교적 적게 발생함. 이 영역에서 객체가 사라질 때 Major GC 라고 지칭함.
	3. Permanent Generation : Perm Generation 혹은 Method Area 라고도 지칭함. 객체나 intern 된 문자열 정보를 저장하는 곳. 이 영역에서도 GC 가 발생할 수 있는데, Major GC 에 포함됨. ([## 참고 : intern 된 문자열이란?](http://seosh81.info/?p=739))

![190244.gif](http://www.cs.rit.edu/~hpb/Jdk5/guide/management/images/generations.gif)

***
### Young Generation
* Young Generation 은 3개의 영역으로 나뉨.
	1. Eden
	2. Survivor 2개
* 새로 생성된 대부분의 객체는 Eden 에 위치.
* Eden 에서 GC 발생 후 살아남은 객체(Old 영역에서 참조) 는  Survivor Generation 중 하나로 이동.
* Eden 에서 GC 발생 시 살아남은 객체가 존재하는 Survivor Generation 으로 객체가 계속 쌓임.
* 하나의 Survivor Generation 이 가득 차면 그 중 살아남은 객체를 다른 Survivor Generation 으로 이동시킴.
* 기존에 가득 찼던 Survivor Generation 은 아무 데이터도 없는 상태로 변경.
* 이 과정을 반복 후에도 살아남은 객체는 Old Generation 으로 이동함.
* Survivor Generation 중 하나는 반드시 비어있어야 함. 그렇지 않다면 비정상적인 상황으로 간주함.

***
### Old Generation
* Old Generation 은 데이터가 가득 차면 GC 를 수행. GC 방식에 따라 절차가 달라짐.
* GC 의 종류는  JDK 7 을 기준으로 5가지.
	1. Serial GC
	2. Parallel GC
	3. Parallel Old GC(Parallel Compacting GC)
	4. Concurrent Mark & Sweep GC(CMS)
	5. G1(Garbage First) GC

---
##### 1. Serial GC (-XX:+UseSerialGC)
* 절대 사용금지. CPU 1코어만 있을때 사용하기 위해 만든 방식. 어플리케이션 성능이 현저히 떨어짐.
* mark-sweep-compact 라는 알고리즘을 사용.
* Old Generation 의 살아있는 객체를 Mark 해 heap 의 앞부분부터 확인후 살아있는것만 남긴(Sweep)다.
* 각 객체들이 연속되게 쌓이도록 힙의 가장 앞부분부터 채워 객체가 존재하는 부분, 없는 부분으로 나눔(Compaction).

![MSC2.png](http://wiki.vivatia.com/images/d/d5/How3.png)

---
##### 2. Parallel GC (-XX:+UseParallelGC)
* Serial GC 와 기본적인 알고리즘은 동일하나 Serial GC 가 하나의 쓰레드로 동작하는 반면 Parallel GC 는 쓰레드가 여러개.

![parallel_GC.png](https://d2.naver.com/content/images/2015/06/helloworld-1329-4.png)

---
##### 3. Parallel Old GC (-XX:+UseParallelOldGC)
* Parallel GC 와 유사하나 mark-sweep-compaction 가 아닌 mark-summary-compaction 단계를 거침.
* 약간 더 복잡한 과정을 거침.

---
##### 4. CMS GC (-XX:+UseConcMarkSweepGC)
* Initial Mark 단계에서 클래스 로더에서 가장 가까운 객체 중 살아있는 객체만 찾는 것으로 끝남. 그러므로 매우 빠름.
* Concurrent Mark 단계에서 방금 살아있다고 확인한 객체에서 참조하고 있는 객체들을 따라가면서 확인. 이 단계의 특징은 다른 쓰레드가 수행중인 상태에서 동작함.
* Remark 단계에서 Concurrent Mark 단계에서 새로 추가되거나 참조가 끊긴  객체를 확인.
* Concurrent Sweep 단계에서 쓰레기를 처리하는 작업을 수행. 이 작업도 다른 쓰레드가 수행중인 상태에서 동작함.
* 장점: 이런 단계로 진행되는 방식이므로 STW 시간이 매우 짧으며,  모든 어플리케이션의 응답 속도가 매우 중요할 때 CMS GC 를 사용. Low Latency GC 라고도 지칭함.
* 단점: 여타 GC 보다 메모리와 CPU 를 더 많이 사용하며 Compaction 단계가 기본적으로 제공되지 않음. 조각난 메모리가 많아 Compaction 작업을 실행하면 다른 GC 의 STW 보다 오래걸리기 때문에 Compaction 작업이 얼마나 자주, 오랫동안 수행되는지 모니터링 해야함.

![GMS_GC.png](https://d2.naver.com/content/images/2015/06/helloworld-1329-5.png)

---
##### 5. G1 GC (-XX:+UseG1GC)
* 일반적인 Young, Old Generation 과는 상이. Young -> Old Generation 의 작업이 사라진 GC 이며, 장기적으로 이슈가 많은 CMS 를 대체하기 위해 만들어짐.
* 바둑판의 각 영역에 객체를 할당하고 GC 를 수행하고, 해당 영역이 꽉 차면 다른 영역에서 객체를 할당하고 GC 를 수행.
* 영역의 목표수치는 2048 개이며 8G 의 Heap 이라면 영역당 4M 가 할당. (8192M/2048 = 4M)
* 영역의 크기는 개발자가 임의 튜닝할 수 있으나(-XX:G1RegionSize, 1M ~ 32M 범위) 추천하지 않음.
* Humongous 영역은 객체가 클 경우(영역의 1/2 혹은 1/3) 사용되는 영역. 이 영역에 대한 GC 는 최적화 되어있지 않으므로 반드시 이 영역을 사용해야 하지 않는 이상 객체의 크기를 줄여 E, S, O 영역 내에 포함이 되도록 하는것이 좋음.
* 지금까지 설명한 어떠한 GC 보다도 성능이 좋지만 JDK 7 에서 정식으로 G1 GC 를 제공.

![g1.png](http://cfile28.uf.tistory.com/image/2137CF34520A29C20E4B3D)

* 상세 내용은 다음 블로그 참고 : **++[G1GC Tistory](http://cfile28.uf.tistory.com/image/2137CF34520A29C20E4B3D)++**

***
### Conclusion
**각 was 에서 생성하는 객체의 크기와 생존 주기 및 장비의 종류도 다양하기 때문에 지속적인 튜닝과 모니터링을 통해서 해당 서비스에 가장 적합한 값을 찾아야 함**

***

### Link
* http://yckwon2nd.blogspot.kr/2014/04/garbage-collection.html
