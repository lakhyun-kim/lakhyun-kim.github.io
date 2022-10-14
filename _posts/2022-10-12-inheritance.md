---
title: 상속(inheritance)
author: lakhyun.kim
categories: [Java]
tags: [Java, 상속, inheritance]
pin: false
---

# 상속의 정의와 장점

기존의 클래스를 **재사용**하여 새로운 클래스를 작성하는 것이다.

**보다 적은 양의 코드**로 새로운 클래스를 작성할 수 있고 **코드를 공통적**으로 관리할 수 있기 때문에 **코드의 추가 및 변경이 매우 용이**하다.

이러한 특징은 코드의 **재사용성**을 높이고 **코드의 중복**을 제거하여 프로그램의 **생산성**과 **유지보수**에 크게 기여한다.

```jsx
class Parent {
	// ...
}

class Child extends Parent { // 상속받고자 하는 클래스의 이름을 extends와 함께 써준다.
	// ...
}
```

상속해주는 클래스를 **조상 클래스**, 상속 받는 클래스를 **자손 클래스**라 하는데 아래와 같은 용어로 표현하기도 한다.

**조상** 클래스 = **부모** 클래스, **상위** 클래스, **기반** 클래스

**자손** 클래스 = **자식** 클래스, **하위** 클래스, **파생된** 클래스

조상 클래스가 변경되면 자손 클래스는 자동적으로 **영향을 받게 되지만**, 자손 클래스가 변경되는 것은 조상 클래스에 **아무런 영향을 주지 못한다.**

- **생성자**와 **초기화 블럭**은 상속되지 않는다. **맴버**만 상속된다.
- 자손 클래스의 맴버 개수는 조상 클래스보다 **항상 같거나 많다.**

```java
class Tv {
	boolean power; // 전원상태(on/off)
	int channel;   // 채널

	void power() { power = !power; }
	void channelUp() { ++channel; }
	void channelDown() { --channel; }
}

class CaptionTv extends Tv {
	boolean caption; // 캡션상태(on/off)
	void displayCaption(String text) {
		if(caption) { // 캡션상태가 on(true)일 때만 text를 보여 준다.
			System.out.println(text);
		}
	}
}

class CaptionTest {
	public static void main(String[] args) {
		CaptionTv ctv = new CaptionTv();
		ctv.channel = 10;                   // 조상 클래스로부터 상속받은 맴버
		ctv.channelUp();                    // 조상 클래스로부터 상속받은 맴버
		System.out.println(ctv.channel);
		ctv.displayCaption("Hello, World");
		ctv.caption = true;                 // 캡션기능을 켠다.
		ctv.displayCaption("Hello, World"); // 캡션을 화면에 보여준다.
	}
}

/*
[실행결과]
11
Hello, World
*/
```

자손 클래스의 인스턴스를 생성하면 조상 클래스의 맴버와 자손 클래스의 맴버가 합쳐진 하나의 인스턴스로 생성된다.

# 클래스간의 관계 - 포함관계

상속이외에도 클래스를 재사용하는 또 다른 방법은 **포함(Composite)관계**를 맺어 주는 것이다.

```java
class Circle {
	Point c = new Point(); // 포함관계
	int r  // 반지름
}

class Point {
	int x; // x좌표
	int y; // y좌표
}
```

# 클래스간의 관계 결정하기

**상속관계**를 맺어 줄 것인지 **포함관계**를 맺어 줄 것인지 결정하는 것은 때때로 혼돈스러울 수 있다.

```java
class Circle {
	Point c = new Point();
	int r;
}
```

```java
class Circle extends Point {
	int r;
}
```

위에 두 경우에 별 차이가 없어 보인다. 그럴 때는 아래처럼 문장을 만들어 보면 클래스 간의 관계가 보다 명확해 진다.

- 원(Circle)은 점(Point)이다. - Circle is a Point
- **원(Circle)은 점(Point)을 가지고 있다. - Circle has a Point**

아래 문장이 더 옳다는 것을 알수 있다. 그래서 위에 관계는 상속관계 보다 **포함관계**를 맺어주는 것이 더 옳다.

- **상속관계**   ‘~은 ~이다.(is-a)’
- **포함관계**   ‘~은 ~을 가지고 있다.(has-a)’

```java
class DrawShape {
	public static void main(String[] args) {
		Point[] p = { new Point(100, 100),
                              new Point(140,  50),
                              new Point(200, 100)
								};
		Triangle t = new Triangle(p);
		Circle c = new Circle(new Point(150, 150), 50);

		t.draw(); // 삼각형을 그린다.
		c.draw(); // 원을 그린다.
	}
}

class Shape {
	String color = "black";
	void draw() {
		System.out.printf("[color=%s]%n", color);
	}
}

class Point {
	int x;
	int y;

	Point(int x, int y) {
		this.x = x;
		this.y = y;
	}

	Point() {
		this(0, 0);
	}

	String getXY() {
		return "{" + x + ", " + y + ")"; // x와 y값을 문자열로 반환
	}
}

class Circle extends Shape {
	Point center; // 원의 원점좌표
	int r; // 반지름

	Circle() {
		this(new Point(0, 0), 100); // Circle(Point center, int r)를 호출
	}

	Circle(Point center, int r) {
		this.center = center;
		this.r = r;
	}

	void draw() { // 원을 그리는 대신에 원의 정보를 출력하도록 했다.
		System.out.printf("[center=(%d, %d), r=%d, color=%s]%n", center.x, center.y, r, color);
	}
}

class Triangle extends Shape {
	Point[] p = new Point[3];

	Triangle(Point[] p) {
		this.p = p;
	}

	void draw() {
		System.out.printf("[p1=%s, p2=%s, p3=%s, color=%s]%n", p[0].getXY(), p[1].getXY(), p[2].getXY(), color);
	}
}

[실행결과]
[p1=(100,100), p2=(140,50), p3=(200,100), color=black]
[center=(150, 150), r=50, color=black]
```

위에 예제로 클래스간의 관계를 맺어보자.

**A Circle is a Shape.      // 1. 원은 도형이다.**
A Circle is a Point.        // 2. 원은 점이다?

A Circle has a Shape.    // 3. 원은 도형을 가지고 있다?
**A Circle has a Shape.   // 4. 원은 점을 가지고 있다.**

1번, 4번 문장이 자연스럽다는 것을 쉽게 알 수 있다. 이렇게 문장을 만들어보면 클래스간의 관계를 결정할 때 감을 잡을 수 있을 것이다.

# 단일 상속(single inheritance)

자바에서는 단일 상속만을 허용한다.

```java
class TVCR extends TB, VCR { // 에러. 조상은 하나만 허용된다.
}
```

# Object클래스 - 모든 클래스의 조상

Object클래스는 모든 클래스 상속계층도의 **최상위**에 있는 조상클래스이다. 다른 클래스로부터 상속 받지 않는 모든 클래스들은 **자동적**으로 Object클래스로부터 상속받게 함으로써 이것을 가능하게 한다.

```java
class Tv {
}
```

위에 코드를 컴파일 하면 컴파일러는 자동적으로 ‘**extends Object**’를 추가하여 Tv클래스가 Object클래스를 상속받도록 한다.
만일 다른 클래스로부터 상속을 받는다고 하더라도 결국 마지막 최상위 조상은 **Object클래스**일 것이다.
