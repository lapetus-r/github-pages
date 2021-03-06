# Semactic Versioniong

## Summary

* Version Number 는 일반적으로 Major.Minor.Patch 형태를 따른다.
* Major Version 은 호환되지 않는 API 변경이 있을 때 증가시킨다.
* Minor Version 은 기 버전과 호환을 유지하며 기능이 추가됐을 때 증가시킨다.
* Patch Version 은 기 버전과 호환을 유지하며 버그를 개선할 때 증가시킨다.
* Pre-release 나 Build Metadate 는 Major.Minor.Patch 형태에 추가적으로 덧붙이는 방식으로 정의한다.

## Specification

* Semantic Versioning 을 사용하는 소프트웨어는 반드시 공개 API를 선언해야 하며, 코드 자체로 선언하거나 문서로 엄격히 명시해야 한다. 공개 API는 정확하고 이해하기 쉬워야 한다.
* 특정 Version 으로 패키지를 명시하고 나면, 그 버전의 내용은 절대 변경하지 말아야 한다. 변경내용은 반드시 새로운 버전으로 배포해야 한다.

##### Major.Minor.Patch

* 일반적으로는 Major.Minor.Patch 의 형태를 띠고 각각은 자연수이며, 0이 앞에 붙어서는 안된다.
* Major 버전이 증가할 때는 Minor 와 Patch 를, Minor 가 증가할 때는 Patch 를 0 으로 초기화한다.
* 공개 API 에 기존과 호환되지 않는 변화가 있을 때는 반드시 Major 를 올린다.
* Major 가 0인 Version 은 초기 개발을 위해서 사용한다. 이 때의 API 는 불안정한 것으로 봐도 무방하다.
* 공개 API 에 기존과 호환되는 새로운 기능을 추가할 때는 반드시 Minor 를 올린다. 공개 API 의 일부를 앞으로 제거(Deprecate)할 것이라 표시한 경우나 내부 비공개 코드에 새로운 기능이 대폭 추가됐을 때, 개선사항이 있을 때도 올릴 수 있다.
* Patch 는 반드시 이전 버전 API 와 호환되는 버그 수정의 경우에만 올린다. 여기서 버그 수정이라 함은 잘못된 내부 기능을 고치는 것이다.
* 1.0.0 부터는 공개 API 를 정의하고 이후 버전번호는 공개 API 에서 어떻게 바뀌는지에 따라 올린다.

```
0.8.2
2.6.33
6.0.37
```

##### pre-release

* Patch 바로 뒤에 "-", "." 를 추가해 정식 배포를 앞둔 pre-release 버전을 표기할 수 있다. 식별자는 아스키(ASCII) 문자, 숫자, "-" 로만 구성한다.
* pre-release Version 은 일반 Version 보다 우선순위가 낮다. 이 버전은 아직 불안정하며 호환성 요구사항이 충족되지 않을 수도 있다.

```
1.0.0-alpha
1.0.0-0.3.7
1.0.0-x.7.z.92
```

##### build metadata

* Patch 나 pre-release 뒤에 "+", "." 를 추가해 build metadata 를 표기할 수 있다. 식별자는 아스키(ASCII) 문자, 숫자, "-" 로만 구성한다.

```
1.0.0-alpha+001
1.0.0+201408080942
1.0.0-beta+exp.sha.5114f84
```

## Compare Version

##### Major.Minor.Patch

* 우선순위는 반드시 Major, Minor, Patch, pre-release 의 식별자를 나누어 계산한다.
* build metadata 는 Version 간 우선순위를 판단할 때 무시해야한다. build metadata 만 다른 두 버전의 우선순위는 같다.
* Major, Minor, Patch 는 숫자로 비교한다.

```
1.0.0 < 2.0.0 < 2.1.0 < 2.1.1
```

##### pre-release

* Major, Minor, Patch 가 모두 동일하나 pre-release 가 표기되어있는 Version 의 우선순위가 낮다.

```
1.0.0-alpha < 1.0.0
```

* Major, Minor, Patch 가 모두 동일하며 pre-release 가 상이할 경우에는 반드시 마침표로 구분된 식별자를 각각 차례로 비교하면서 차이점을 찾는다.
* 숫자로만 구성된 식별자는 수의 크기로 비교한다.
* 문자열, "-" 가 있는 경우에는 아스키(ASCII) 문자열로 비교한다.
* 숫자로만 구성된 식별자는 어떤 경우에도 문자열과 "-" 로 구성되어 있는 식별자보다 낮은 우선순위를 갖는다.
* 앞선 식별자가 모두 같은 pre-release Version 은 필드가 많은 쪽이 높은 우선순위를 갖는다.

```
1.0.0-alpha < 1.0.0-alpha.1 < 1.0.0-alpha.beta < 1.0.0-beta < 1.0.0-beta.2 < 1.0.0-beta.11 < 1.0.0-rc.1 < 1.0.0.
```

##### Compare Library
* https://github.com/npm/node-semver
* https://github.com/k-bx/python-semver
* https://github.com/iantruslove/SemverStringer

## With GitFlow

##### Question
* Version 변경이 무엇을 의미하는가?
* 이전 Version 호환성을 깨뜨리는가, 그렇지 않은가?
* 어떤 Branch 로부터 해당 Version 이 생성되었을까?
* 어떤 환경에 배포될수 있는가?

```
1. foobar-1.0.0-SNAPSHOT20120512
2. foobar-1.0.0 -> foobar-1.0.1
3. foobar-1.0.1 -> foobar-1.0.2-rc1
4. foobar-1.0.2 -> foobar-1.1.0-rc1
5. foobar-1.2.0 -> foobar-2.0.0
```
##### Answer
* http://therebelrobot.github.io/HubFlow-Site/build/#/examples
