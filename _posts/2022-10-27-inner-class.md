---
title: 내부 클래스(inner class)
author: lakhyun.kim
categories: [Java]
tags: [Java, 내부 클래스, inner class]
pin: false
---

# 내부 클래스란?

내부 클래스는 클래스 내에 선언된 클래스이다. 클래스에 다른 클래스를 선언하는 이유는 두 클래스가 서로 긴밀한 관계에 있기 때문이다.

```java
class A { // 외부 클래스
	// ...
	class B { // 내부 클래스
		// ...
	}
	// ...
}
```

## 내부클래스의 장점

- 내부 클래스에서 외부클래스의 맴버들을 쉽게 접근할 수 있다.
- 코드의 복잡성을 줄일 수 있다.(캡슐화)

# 내부 클래스의 종류와 특징

내부 클래스의 종류는 변수의 선언위치에 따른 종류와 같다.

| 내부 클래스 | 특징 |
| --- | --- |
| 인스턴스 클래스(instance class) | 외부 클래스의 멤버변수 선언위치에 선언하며, 외부 클래스의 인스턴스멤버처럼 다루어진다. 주로 외부 클래스의 인스턴스멤버들과 관련된 작업에 사용될 목적으로 선언한다. |
| 스태틱 클래스(static class) | 외부 클래스의 멤버변수 선언위치에 선언하며, 외부 클래스의 static멤버처럼 다루어진다. 주로 외부 클래스의 static멤버, 특히 static메서드에서 사용될 목적으로 선언한다. |
| 지역 클래스(local class) | 외부 클래스의 메서드나 초기화블럭 안에 선언하며, 선언된 영역 내부에서만 사용될 수 있다. |
| 익명 클래스(anonymous class) | 클래스의 선언과 객체의 생성을 동시에 하는 이름없는 클래스(일회용) |

# 내부 클래스의 선언

변수가 선언된 위치에 따라 인스턴스변수, 클래스변수(static변수), 지역변수로 나뉘듯이 내부 클래스도 이와 마찬가지로 선언된 위치에 따라 나뉘고 각 내부 클래스의 선언위치에 따라 같은 선언위치에 변수와 동일한 유효범위(scope)와 접근성(accessibility)을 갖는다.

```java
class Outer {
	int iv = 0;
	static int cv = 0;

	void myMethod() {
		int lv = 0;
	}
}
```

```java
class Outer {
	class InstanceInner { }
	static class StaticInner { }

	void myMethod() {
		class LocalInner { }
	}
}
```

# 내부 클래스의 제어자와 접근성

내부 클래스도 클래스이기 때문에 abstract나 final과 같은 **제어자**를 사용할 수 있을 뿐만 아니라, 멤버변수들처럼 private, protected과 같은 **접근제어자**도 사용이 가능하다.

**static클래스만 static멤버를 가질 수 있다.** 다만, final과 static이 동시에 붙은 변수는 상수이므로 모든 내부 클래스에서 정의가 가능하다.

인스턴스클래스는 스태틱 클래스의 멤버들을 객체생성 없이 사용할 수 있지만, **스태틱 클래스는 인스턴스클래스의 멤버들을 객체생성 없이 사용할 수 없다.**

아래는 내부 클래스에서 외부 클래스의 변수들에 대한 **접근성**을 보여주는 예제이다.

```java
class InnerEx3 {
	private int outerIv = 0;
	static int outerCv = 0;

	class InstanceInner {
		int iiv = outerIv; // 외부 클래스의 private멤버도 접근가능하다.
		int iiv2 = outerCv;
	}

	static class StaticInner {
		// 스태틱 클래스는 외부 클래스의 인스턴스멤버에 접근 할 수 없다.
		// int siv = outerIv; // 에러
		static int scv = outerCv;
	}

	void myMethod() {
		int iv = 0;
		final int LV = 0; // JDK1.8부터 final 생략 가능

		class LocalInner {
			int liv = outerIv;
			int liv2 = outerCv;
			// 외부 클래스의 지역변수는 final이 붙은 변수(상수)만 접근가능하다.
			// int liv3 = lv;   // 에러!!!(JDK1.8부터 에러 아님)
			int liv4 = LV;      // OK
		}
	}
}
```

컴파일 했을 때 생성되는 파일명은 ‘**외부 클래스명$내부 클래스명.class**’형식으로 되어 있다.

```java
class Outer {
	int value = 10;  // Outer.this.value

	class Inner {
		int value = 20; // this.value
		void method1() {
			int value = 30;
			System.out.println("           value : " + value);
			System.out.println("      this.value : " + this.value);
			System.out.println("Outer.this.value : " + Outer.this.value);
		}
	}
}

class InnerEx5 {
	public static void main(String[] args) {
		Outer outer = new Outer();
		outer.Inner inner = outer.new Inner();
		inner.method1();
	}
}

/*
[실행결과]
           value : 30
      this.value : 20
Outer.this.value : 10
*/
```

내부 클래스와 외부 클래스에 선언된 변수의 이름이 같을 때 변수 앞에 **this** 또는 **외부클래스명.this**를 붙여서 서로 구별할 수 있다.

# 익명 클래스(**anonymous class)**

이름이 없고 클래스의 선언과 객체의 생성을 동시에 하기 때문에 단 한번만 사용될 수 있고 오직 하나의 객체만을 생성할 수 있는 **일회용 클래스**이다.

```java
new 조상클래스이름() {
	// 멤버 선언
}
또는
new 구현인터페이스이름() {
	// 멤버 선언
}
```

이름이 없기 때문에 생성자도 가질 수 없으며, 오로지 단 하나의 클래스를 상속받거나 단 하나의 인터페이스만을 구현할 수 있다.

```java
class InnerEx6 {
	Object iv = new Object() { void method() { } };        // 익명클래스
	static Object cv = new Object() { void method() { } }; // 익명클래스

	void myMethod() {
		Object lv = new Object() { void method() { } };      // 익명클래스
	}
}
```

아래 예제를 실행하면 아무것도 나타나지 않는다. 단지 익명클래스로 변환하는 예를 보여주기 위한 예제다.

```java
import java.awt.*;
import java.awt.event.*;

class InnerEx7 {
	public static void main(String[] args) {
		Button b = new Button("Start");
		b.addActionListener(new EventHandler());
	}
}

class EventHandler implements ActionListener {
	public void actionPerformed(ActionEvenet e) {
		System.out.println("ActionEvent occurred!!!");
	}
}

class InnerEx8 {
	public static void main(String[] args) {
		Button b = new Button("Start");
		b.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvenet e) {
				System.out.println("ActionEvent occurred!!!");
			}
		}); // 익명클래스 끝
	} // main 끝
}
```

InnerEx7, EventHandler를 익명클래스를 이용해서 변경한 것이 InnerEx8이다. 먼저 두 개의 독립된 클래스를 작성한 다음에, 다시 익명클래스를 이용하여 변경하면 보다 쉽게 코드를 작성할 수 있다.

# 출처

자바의 정석
