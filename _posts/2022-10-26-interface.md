---
title: 인터페이스(interface)
author: lakhyun.kim
categories: [Java]
tags: [Java, 인터페이스, interface]
pin: false
---

# 인터페이스란?

인터페이스는 **일종의 추상클래스**이지만 일반메서드 또는 맴버변수를 가질 수 없고, 오직 **추상메서드**와 **상수**만을 맴버로 가질 수 있으며, 그 외의 다른 어떠한 요소도 허용하지 않는다.

추상클래스를 **미완성 설계도**라고 한다면, 인터페이스는 구현된 것은 아무 것도 없고 밑그림만 그려져있는 **기본 설계도**라 할 수 있다.

# 인터페이스의 작성

클래스를 작성하는 것과 같다. 다만 키워드로 class 대신 interface를 사용한다. 그리고 접근제어자로 public 또는 default를 사용할 수 있다.

```java
interface 인터페이스이름 {
	public static final 타입 상수이름 = 값;
	public abstract 메서드이름(매개변수목록);
}
```

## 인터페이스 맴버들의 제약사항

- 모든 맴버변수는 **public static final** 이어야 하며, 이를 생략할 수 있다.
- 모든 메서드는 **public abstract** 이어야 하며, 이를 생략할 수 있다.

  단, static메서드와 default메서드는 예외(JDK1.8부터 변경)


생략된 제어자는 컴파일 시에 컴파일러가 자동적으로 추가해준다.

```java
interface PlayingCard {
	public static final int SPADE = 4;
	final int DIAMOND = 3;        // public static final int DIAMOND = 3;
	static int HEART = 2;         // public static final int HEART = 2;
	int CLOVER = 1;               // public static final int CLOVER = 1;

	public abstract String getCardNumber();
	String getCardKind();         // public abstract String getCardKind();
}
```

원래는 인터페이스의 모든 메서드는 **추상메서드**이어야 하는데, JDK1.8부터 인터페이스에 **static메서드**와 **default메서드**의 추가를 허용하는 방향으로 변경되었다.

# 인터페이스의 상속

인터페이스는 인터페이스로부터만 상속받을 수 있으며, 클래스와 달리 **다중상속**이 가능하다.

```java
interface Movable {
	/* 지정된 위치로 이동하는 기능의 메서드 */
	void move(int x, int y);
}

interface Attackable {
	/* 지정된 대상을 공격하는 기능의 메서드 */
	void attack(Unit u);
}

interface Fightable extends Movable, Attackable { }
```

# 인터페이스의 구현

인터페이스도 추상클래스처럼 그 자체로는 인스턴스를 생성할 수 없으며, 추상클래스가 상속을 통해 추상메서드를 완성하는 것처럼, 인터페이스도 다르지 않다. 다만 클래스는 확장한다는 의미로 **extends**를 사용하지만 인터페이스는 구현한다는 의미로 **implements**를 사용한다.

```java
class 클래스이름 implements 인터페이스이름 {
	// 인터페이스에 정의된 추상메서드를 구현해야 한다.
}

class Fighter implements Fightable {
	public void move(int x, int y) { /* 내용 생략 */ }
	public void attack(Unit) { /* 내용 생략 */ }
}
```

만일 인터페이스의 메서드 중 일부만 구현한다면, **추상클래스**로 선언해야 한다.

```java
abstract class Fighter implements Fightable {
	public void move(int x, int y) { /* 내용 생략 */ }
}
```

그리고 다음과 같이 **상속**과 **구현**을 동시에 할 수도 있다.

```java
class Fighter extends Unit implements Fightable {
	public void move(int x, int y) { /* 내용 생략 */ }
	public void attack(Unit) { /* 내용 생략 */ }
}
```

# 인터페이스를 이용한 다중상속

두 조상으로부터 상속받은 맴버 중에서 맴버변수의 이름이 같거나 메서드의 선언부가 일치하고 구현 내용이 다르다면 이 두 조상으로부터 상속받는 자손클래스는 어느 조상의 것을 상속받게 되는 것인지 알 수 없다.

그래서 다중상속은 장점도 있지만 단점이 더 크다고 판단하였기 때문에 **자바에서는 다중상속을 허용하지 않는다.** 그러나 또 다른 객체지향언어인 C++에서는 다중상속을 허용하기 때문에 자바는 다중상속을 허용하지 않는다는 것이 단점으로 부각되는 것에 대한 대응으로 자바도 인터페이스를 이용하면 다중상속이 가능하다라고 하는 것일 뿐 **자바에서 인터페이스로 다중상속을 구현하는 경우는 거의 없다.**

인터페이스는 static상수만 정의할 수 있으므로 조상클래스의 맴버변수와 충돌하는 경우는 거의 없고 충돌된다 하더라도 클래스 이름을 붙여서 구분이 가능하다. 그리고 추상메서드는 구현내용이 전혀 없으므로 조상클래스의 메서드와 선언부가 일치하는 경우에는 당연히 조상클래스 쪽의 메서드를 상속받으면 되므로 문제가되지 않는다.

그러나, 이렇게 하면 상속받는 맴버의 충돌은 피할 수 있지만, **다중상속의 장점을 잃게된다. 만일 두 개의 클래스로부터 상속을 받아야 할 상황이라면,** 두 조상클래스 중에서 비중이 높은 쪽을 선택하고 다른 한쪽은 클래스 내부에 맴버로 포함시키는 방식으로 처리하거나 어느 한쪽의 필요한 부분을 뽑아서 인터페이스로 만든 다음 구현하도록 한다.

**예를 들어,** Tv클래스와 VCR클래스가 있을 때, TVCR클래스를 작성하기 위해 한 쪽만 선택하여 상속받고 나머지 한 쪽은 클래스 내부에 포함시켜서 내부적으로 인스턴스를 생성해서 사용한다.

```java
public class Tv {
	protected boolean power;
	protected int channel;
	protected int volume;

	public void power() { power = !power; }
	public void channelUp() { channel++; }
	public void channelDown() { channel--; }
	public void volumeUp() { volume++; }
	public void volumeDown() { volume--; }
}

public class VCR {
	protected int counter; // VCR의 카운터

	public void play() {
		// Tape을 재생한다.
	}
	public void stop() {
		// 재생을 멈춘다.
	}
	public void reset() {
		counter = 0;
	}
	public int getCounter() {
		return counter;
	}
	public void setCounter(int c) {
		counter = c;
	}
}
```

VCR클래스에 정의된 메서드와 동일하게 추상메서드를 갖는 **인터페이스**를 작성한다.

```java
public interface IVCR {
	public void play();
	public void stop();
	public void reset();
	public int getCounter();
	public void setCounter(int c);
}
```

IVCR 인터페이스를 구현하고 Tv클래스로부터 상속받는 **TVCR클래스**를 작성한다.

이때 VCR클래스 타입의 참조변수를 맴버변수로 선언하여 IVCR인터페이스의 추상메서드를 구현하는데 사용한다.

```java
public class TVCR extends Tv implements IVCR {
	VCR vcr = new VCR();

	public void play() {
		vcr.play();  // 코드를 작성하는 대신 VCR인스턴스의 메서드를 호출한다.
	}
	public void stop() {
		vcr.stop();
	}
	public void reset() {
		vcr.reset();
	}
	public int getCounter() {
		vcr.getCounter()
	}
	public void setCounter(int c) {
		vcr.setCounter(c);
	}
}
```

IVCR인터페이스를 구현하기 위해서는 새로 메서드를 작성해야하는 부담이 있지만 이처럼 VCR클래스의 인스턴스를 사용하면 손쉽게 **다중상속**을 구현할 수 있다.

# 인터페이스를 이용한 다형성

다형성에 대해 학습할 때 자손클래스의 인스턴스를 조상타입의 참조변수로 참조하는 것이 가능하다는 것을 배웠다. 인터페이스 역시 가능하다.

인터페이스 Fightable을 클래스 Fighter가 구현했을 때, 다음과 같이 Fighter인스턴스를 Fightable타입의 참조변수로 참조하는 것이 가능하다.

```java
Fightable f = (Fightable)new Fighter();
또는
Fightable f = new Fighter();
```

```java
interface Parseable {
	// 구문 분석작업을 수행한다.
	public abstract void parse(String fileName);
}

class ParserManager {
	// 리턴타입이 Parseable인터페이스이다.
	public static Parseable getParser(String type) {
		if(type.equals("XML")) {
			return new XMLParser();
		} else {
			return new HTMLParser();
		}
	}
}

class XMLParser implements Parseable {
	public void parse(String fileName) {
		/* 구문 분석작업을 수행하는 코드를 적는다. */
		System.out.println(fileName + " - XML parsing completed.");
	}
}

class HTMLParser implements Parseable {
	public void parse(String fileName) {
		/* 구문 분석작업을 수행하는 코드를 적는다. */
		System.out.println(fileName + " - HTML parsing completed.");
	}
}

class ParserTest {
	public static void main(String[] args) {
		Parseable parser = ParserManage.getParser("XML");
		parser.parse("document.xml");
		Parseable parser = ParserManage.getParser("HTML");
		parser.parse("document2.xml");
	}
}

/*
[실행결과]
document.xml - XML parsing completed.
document2.xml - HTML parsing completed.
*/
```

ParserManager클래스의 getParser메서드는 매개변수로 넘겨받은 type의 값에 따라 XMLParser인스턴스 또는 HTMLParser인스턴스를 반환한다.

만일 나중에 새로운 종류의 XML구문분석기 NewXMLParser클래스가 나와도 ParserTest클래스는 변경할 필요 없이 ParserManager클래스의 getParser메서드에서 **return new XMLParser();** 대신 **return new NewXMLParser();로** 변경하기만 하면 된다.

이러한 장점은 특히 분산환경 프로그래밍에서 그 위력을 발휘한다. 사용자 컴퓨터에 설치된 프로그램을 변경하지 않고 서버측의 변경만으로도 사용자가 새로 개정된 프로그램을 사용하는 것이 가능하다.

# 인터페이스의 장점

1. **개발시간을 단축시킬 수 있다.**

   일단 인터페이스가 작성되면 이를 사용해서 프로그램을 작성하는 것이 가능하다. 메서드를 호출하는 쪽에서는 메서드의 내용에 관계없이 **선언부**만 알면 되기 때문이다.

   그리고 동시에 다른 한 쪽에서는 인터페이스를 **구현하는 클래스**를 작성하도록 하여, 인터페이스를 구현하는 클래스가 작성될 때까지 기다리지 않고도 **양쪽에서 동시에 개발을 진행할 수 있다.**

2. **표준화가 가능하다.**

   프로젝트에 사용되는 기본 틀을 인터페이스로 작성한 다음, 개발자들에게 인터페이스를 구현하여 프로그램을 작성하도록 함으로써 보다 **일관되고 정형화된 프로그램의 개발이 가능하다.**

3. **서로 관계없는 클래스에게 관계를 맺어 줄 수 있다.**

   서로 상속관계에 있지도 않고, 같은 조상클래스를 가지고 있지 않은 서로 아무런 관계도 없는 클래스들에게 하나의 인터페이스를 공통적으로 구현하도록 함으로써 **관계를 맺어 줄 수 있다.**

4. **독립적인 프로그래밍이 가능하다.**

   인터페이스를 이용하면 **클래스의 선언과 구현을 분리시킬 수 있기 때문에** 실제구현에 독립적인 프로그램을 작성하는 것이 가능하다. 클래스와 클래스간의 직접적인 관계를 인터페이스를 이용해서 **간접적인 관계로 변경하면,** 한 클래스의 변경이 관련된 다른 클래스에 영향을 미치지 않는 독립적인 프로그래밍이 가능하다.


```java
class RepairableTest {
	public static void main(String[] args) {
		Tank tank = new Tank();
		Dropship dropship = new Dropship();

		Marine marine = new Marine();
		SCV scv = new SCV();

		scv.repair(tank);    // SCD가 Tank를 수리하도록 한다.
		scv.repair(dropship);
//		scv.repair(marine);    // 에러!
	}
}

interface Repairable { }

class GroundUnit extends Unit {
	GroundUnit(int hp) {
		super(hp);
	}
}

class AirUnit extends Unit {
	AirUnit(int hp) {
		super(hp);
	}
}

class Unit {
	int hitPoint;
	final int MAX_HP;
	Unit(int hp) {
		MAX_HP = hp;
	}
	// ...
}

class Tank extends GroundUnit implements Repairable {
	Tank() {
		super(150);     // Tank의 HP는 150이다.
		hitPoint = MAX_HP;
	}

	public String toString() {
		return "Tank";
	}
	// ...
}

class Dropship extends AirUnit implements Repairable {
	Dropship() {
		super(125);     // Dropship의 HP는 125이다.
		hitPoint = MAX_HP;
	}

	public String toString() {
		return "Dropship";
	}
	// ...
}

class Marine extends GroundUnit {
	Marine() {
		super(40);
		hitPoint = MAX_HP;
	}
	// ...
}

class SCV extends implements Repairable {
	SCV() {
		super(60);
		hitPoint = MAX_HP;
	}

	void repair(Repairable r) {
		if(r instanceof Unit) {
			Unit u = (Unit)r;
			while(u.hitPoint != u.MAX_HP) {
				/* Unit의 HP를 증가시킨다. */
				u.hitPoint++;
			}
			System.out.println(u.toString() + "의 수리가 끝났습니다.");
		}
	}
	// ...
}

/*
[실행결과]
Tank의 수리가 끝났습니다.
Dropship의 수리가 끝났습니다.
*/
```

# 인터페이스의 이해

- 클래스를 사용하는 쪽(User)과 클래스를 제공하는 쪽(Provider)이 있다.
- 메서드를 사용(호출)하는 쪽(User)에서는 사용하려는 메서드(Provider)의 선언부만 알면 된다.(내용은 몰라도 된다.)

```java
class A {
	public void methodA(B b) {
		b.methodB();
	}
}

class B {
	public void methodB() {
		System.out.println("methodB()");
	}
}

class InterfaceTest {
	public static void main(String[] args) {
		A a = new A();
		a.methodA(new B());
	}
}

/*
[실행결과]
methodB()
*/
```

위와 같이 클래스 A(User)는 클래스B(Provider)의 인스턴스를 생성하고 메서드를 호출한다. 이 두 클래스는 서로 **직접적인 관계**가 있다.

이와 같이 직접적인 관계의 두 클래스는 **한 쪽(Provider)이 변경되면 다른 한 쪽(User)도 변경되어야 한다는 단점**이 있다.

그러나 **인터페이스**를 매개체로 해서 메서드에 접근하도록 하면, 클래스 B에 변경사항이 생겨도 클래스 A는 전혀 영향을 받지 않도록 하는 것이 가능하다.

```java
class A {
	void autoPlay(I i) {
		i.play();
	}
}

interface I {
	public abstract void play();
}

class B implements I {
	public void play() {
		System.out.println("play in B class");
	}
}

class C implements I {
	public void play() {
		System.out.println("play in C class");
	}
}

class InterfaceTest2 {
	public static void main(String[] args) {
		A a = new A();
		a.autoPlay(new B()); // void autoPlay(I i) 호출
		a.autoPlay(new C()); // void autoPlay(I i) 호출
	}
}

/*
[실행결과]
play in B class
play in C class
*/
```

**위와 같이 클래스 A를 작성하는데 클래스 B가 관련되지 않았다는 사실에 주목하자.**

Thread의 생성자인 **Thread(Runnable target)이** 이런 방식으로 되어 있다.

이처럼 매개변수를 통해 동적으로 제공받을 수 도 있지만 다음과 같이 제 3의 클래스를 통해서 제공받을 수도 있다. **JDBC의 DriverManager클래스**가 이런 방식으로 되어 있다.

```java
class InterfaceTest3 {
	public static void main(String[] args) {
		A a = new A();
		a.methodA();
	}
}

class A {
	void methodA() {
		I i = InstanceManager.getInstance(); // 제 3의 클래스의 메서드를 통해서 인터페이스 I를 구현한 클래스의 인스턴스를 얻어온다.
		i.methodB();
		System.out.println(i.toString()); // i로 Object클래스의 메서드 호출가능
	}
}

interface I {
	public abstract void methodB();
}

class B implements I {
	public void methodB() {
		System.out.println("methodB in B class");
	}

	public String toString() { return "class B"; }
}

class InstanceManager {
	public static I getInstance() {
		return new B();
	}
}

/*
[실행결과]
methodB in B class
class B
*/
```

인스턴스를 직접 생성하지 않고, getInstance()라는 메서드를 통해 제공받는다. 이렇게 하면, 나중에 다른 클래스의 인스턴스로 변경되어도 A클래스의 변경없이 getInstance()만 변경하면 된다는 장점이 생긴다.

# 디폴트 메서드와 static메서드

원래는 인터페이스에 **추상메서드**만 선언할 수 있는데, JDK1.8부터 **디폴트메서드**와 **static메서드**도 추가할 수 있게 되었다.

**static메서드**는 인스턴스와 관계가 없는 독립적인 메서드이기 때문에 추가하지 못할 이유가 없었지만 자바를 보다 쉽게 배울 수 있도록 규칙을 단순히 할 필요가 있었다. 접근 제어자가 항상 public이며, 생략할 수 있다.

조상클래스에 새로운 메서드를 추가하는 것은 별 일이 아니지만, 인터페이스의 경우에는 이 인터페이스를 구현한 기존의 모든 클래스들이 새로 추가된 메서드를 구현해야 하기 때문에 **디폴트메서드**를 고안해 내었다.

**디폴트메서드**는 추상메서드의 기본적인 구현을 제공하는 메서드로, 추상메서드가 아니기 때문에 새로 추가되어도 해당 인터페이스를 구현한 클래스를 변경하지 않아도 된다. 그리고 메서드 앞에 default를 붙이며 몸통{}이 있어야 한다. 접근제어자가 public이며, 생략할 수 있다.

새로 추가된 디폴트메서드가 기존의 메서드와 **이름이 중복되어 충돌**하는 경우가 발생한다. 이 충돌을 해결하는 규칙은 다음과 같다.

1. 여러 인터페이스의 디폴트메서드 간의 충돌
  - 인터페이스를 구현한 클래스에서 디폴트메서드를 **오버라이딩**해야한다.
2. 디폴트 메서드와 조상클래스의 메서드 간의 충돌
  - 조상클래스의 메서드가 **상속**되고, 디폴트 메서드는 무시된다.

```java
class DefaultMethodTest {
	public static void main(String[] args) {
		Child c = new Child();
		c.method1();
		c.method2();
		MyInterface.staticMethod();
		MyInterface2.staticMethod();
	}
}

class Child extends Parent implements MyInterface, MyInterface2 {
	public void method1() {
		System.out.println("method1() in Child"); // 오버라이딩
	}
}

class Parent {
	public void method2() {
		System.out.println("method2() in Parent");
	}
}

interface MyInterface {
	default void method1() {
		System.out.println("method1() in MyInterface");
	}
	default void method2() {
		System.out.println("method2() in MyInterface");
	}
	static void staticMethod() {
		System.out.println("staticMethod() in MyInterface");
	}
}

interface MyInterface2 {
	default void method1() {
		System.out.println("method1() in MyInterface2");
	}
	static void staticMethod() {
		System.out.println("staticMethod() in MyInterface2");
	}
}

/*
[실행결과]
method1() in Child
method2() in Parent
staticMethod() in MyInterface
staticMethod() in MyInterface2
*/
```

# 출처

자바의 정석
