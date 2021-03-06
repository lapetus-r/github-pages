# Test Driven Development

---

* TDD
* Purpose
* Principle
* JUnit
* Hamcrest
* @Before, @After, @BeforeClass, @AfterClass
* Given/When/Then Pattern
* Mock Framework, Mockito
* Environment

---

## TDD

* "업무 코드를 작성하기 전 테스트 코드를 먼저 만드는 것!"

## Purpose

* 론 제프리(Ron Jeffries)

```code
잘 동작하는 깔끔한 코드 - Clean code that works
```

## Principle

* 로버트 마틴(Robert C. Martin)

```code
	1. 실패하는 테스트를 작성하기 전에는 절대로 제품 코드를 작성하지 않는다.
    2. 실패하는 테스트 코드를 한 번에 하나 이상 작성하지 않는다.
    3. 현재 실패하고 있는 테스트를 통과하기에 충분한 정도를 넘어서는 제품 코드를 작성하지 않는다.
```

## JUnit

* Test Fixture Method: 테스트를 반복적으로 수행할 수 있게 도와주며 매번 동일한 결과를 얻을수 있게 해주는 일관된 테스트 실행환경

```java
    setUp() -> test() -> tearDown()
```
* Assertions: 테스트 케이스의 수행 결과를 판별해주는 단정문

``` java
import static org.junit.Assert.*;

assertEquals([message], expected, actual)
assertArrayEqauls[message], expected, actual)
assertTrue([message], expected)
assertFalse([message], expected)
assertSame([message], expected, actual)
assertNull([message], expected)
assertThat([message], expected)
fail([message])
```
* Test Runner: 테스트 실행

``` java
@RunWith(SomeClass.class)
```

## Hamcrest

* jMock 이라는 Mock 라이브러리 저자들이 참여해 만들고 있는 Matcher 라이브러리
* Hamcrest 는 assertEquals 보다 assertThat 사용을 권장. 보다 더 문맥적인 흐름을 만들어준다고 여기기 때문

``` java
import static org.hamcrest.CoreMatchers.*;

assertThat(result, is(not(expected));
assertThat(result, nullValue(expected));
```

## @Before, @After, @BeforeClass, @AfterClass

* 테스트 클래스 전체에서 참조할 컨텍스트를 위치
* @BeforeClass, @AfterClass 는 static 으로 작성

![image](http://1.bp.blogspot.com/-1zmilP-MNfE/UjVyAcziSeI/AAAAAAAAApc/UancmQS4Mps/s1600/junit4+Fixture+Method.001.001.jpg)

```java
@Before
public void setUp() {
	doSomething();
}

@After
public void tearDown() {
	doSomething();
}

@BeforeClass
public static void init() {
	doSomething();
}

@AfterClass
public static void destroy() {
	doSomething();
}
```

## Given/When/Then Pattern

* [What is Given/When/Then?](http://guide.agilealliance.org/guide/gwt.html)
* BDD 스타일을 따르는 템플릿
* Given/When/Then 주석을 달자
	* Given: 테스트 케이스에서 사용될 변수 선언(선행 조건)
	* When: 테스트 대상 메서드 호출, 결과 저장(기능 수행)
	* Then: 테스트 결과 확인
* [소프트웨어 레벨 85 에 빨리 오르는 방법](http://monkeyisland.pl/2009/12/07/given-when-then-forever)

## Mock Framework, Mockito

* [What is Mockito?](http://docs.mockito.googlecode.com/hg/1.9.5/org/mockito/runners/MockitoJUnitRunner.html)
* Mockito 사용 시점
	1. 테스트 작성을 위한 환경 구축이 어려워서
	2. 테스트가 특정 경우가 순간에 의존적이라서
	3. 테스트 시간이 오래걸려서
* Mock?
	* 행위를 검증하기 위해 사용되는 객체

```java
@RunWith(MockitoJUnitRunner.class)

@InjectMocks
private UserService userService = new UserService();

@Mock
private UserDao userDao;
```

* When, ThenReturn

```java
when(userDao.getAge()).thenReturn(30);
```

* Verify, [Method]

```java
verify(userDao, times(3)).getAge();
```

## Environment

```xml
<dependencies>
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.11</version>
        <scope>test</scope>
    </dependency>

    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <version>0.11.6</version>
        <scope>provided</scope>
    </dependency>

    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>jcl-over-slf4j</artifactId>
        <version>1.7.2</version>
    </dependency>

    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-api</artifactId>
        <version>1.7.5</version>
    </dependency>

    <dependency>
        <groupId>ch.qos.logback</groupId>
        <artifactId>logback-classic</artifactId>
        <version>1.1.1</version>
    </dependency>

    <dependency>
        <groupId>commons-lang</groupId>
        <artifactId>commons-lang</artifactId>
        <version>2.6</version>
    </dependency>

    <dependency>
        <groupId>org.mockito</groupId>
        <artifactId>mockito-all</artifactId>
        <version>1.9.5</version>
    </dependency>

</dependencies>
```