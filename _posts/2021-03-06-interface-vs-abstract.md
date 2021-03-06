# 추상클래스(abstract class)
* 추상클래스는 추상 메서드가 하나 이상 포함되는 클래스다. 여기서 추상 메서드라 함은 메서드의 선언부만 있고 본문이 없는것을 말한다.
```abstract public void test(int a);```
* 추상클래스를 상속받은 자식클래스는 반드시 추상메소드를 오버라이딩 해야한다. 강제구현을 요구할 때 자주 쓰임.

# 인터페이스(interface)
* 인터페이스는 추상 메서드만으로 이루어진 클래스를 말한다. 고도화된 추상 클래스.
  ```java
  public void test(int a);
  ```

# 공통점
* abtract class와 interface는 둘 다 자체로 인스턴스화 될 수 없다.
* 구현부가 없는 메서드를 소유할 수 있다.

# 차이점
* 인터페이스를 사용하는 가장 큰 이유는 다중상속(implements)이 가능하기 때문이다.

```java
public class Tiger extends Cat {
  @Override public void eat() {
    // ...구현부...
  }
}

public abstract class Cat {
  public abstract void eat();
}
```
```java
public class CampingCar implements Vehicle, Toilet, (...etc) {
  @Override public void run(void) {
    // ...구현부...
  }
  
  @Override public void flush(void) {
    // ...구현부...
  }
}

public interface Vehicle {
  public void run();
}

public interface Toilet {
  public void flush();
}
```
* abstract를 받는(extends) 클래스는 "순수상속"을 받는다고 하고, interface를 받는(implements) 클래스는 "구현상속"을 받는다고 한다.
* abstract class로부터의 상속은 부모로부터의 상속이라고 할 수 있고, interface로부터의 상속은 조언자로부터의 상속이라고 할 수 있다.

---

***abstract class는 작업의 레벨 분할을 위해서 사용하고, interface는 공동 작업을 위한 상호간의 인터페이스를 위해서 사용된다.
전문적인 용어로 상속(extends)은 서브클래싱을 의미하고 구현(implements)은 서브타이핑을 의미한다. 여기서 서브클래싱은 상속을 통해 기능을 구현하는것을 의미하며, 서브타이핑은 기능을 공통적인 타입으로 묶어주는것을 의미한다.***

---
