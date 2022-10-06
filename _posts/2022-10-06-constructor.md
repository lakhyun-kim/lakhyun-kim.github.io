---
title: 생성자(constructor)
author: lakhyun.kim
categories: [Java]
tags: [Java, 생성자, constructor]
pin: false
---

# 생성자란?

인스턴스가 생성될 때 호출되는 **인스턴스 초기화 메서드**이다. 따라서 인스턴스 변수의 초기화 작업에 주로 사용되며, 인스턴스 생성 시에 실행되어야 할 작업을 위해서도 사용된다.

## 생성자의 조건

1. 생성자의 이름은 클래스의 이름과 같아야 한다.
2. 생성자는 리턴 값이 없다.

```java
class Card {
	Card() { // 매개변수가 없는 생성자
	}

	Card(String k, int num) { // 매개변수가 있는 생성자
	}
}
```

## 인스턴스 생성이 수행되는 과정

```java
Card c = new Card();
```

1. 연산자 new에 의해서 메모리(heap)에 Card클래스의 인스턴스가 생성된다.
2. 생성자 Card()가 호출되어 수행된다.
3. 연산자 new의 결과로, 생성된 Card인스턴스의 주소가 반환되어 참조변수 c에 저장된다.

# 기본 생성자(default constructor)

모든 클래스에는 하나 이상의 생성자가 정의되어 있어야 한다. 하지만 생성자를 정의하지 않고도 인스턴스를 생성할 수 있었던 이유는 컴파일러가 **기본 생성자**를 제공해 주기 때문이다. 기본 생성자는 매개변수를 하나도 가지지 않으며, 아무런 명령어도 포함하고 있지 않다.

```java
클래스이름() {
}

Card() {
}
```

기본 생성자가 컴파일러에 의해서 추가되는 경우는 **클래스에 정의된 생성자가 하나도 없을 때 뿐이다.**

# 매개변수가 있는 생성자

생성자도 메서드처럼 매개변수를 선언하여 호출 시 값을 넘겨받아서 **인스턴스의 초기화 작업**에 사용할 수 있다.

```java
class Car {
	String color; // 색상
	String gearType; // 변속기 종류 - auto(자동), manual(수동)
	int door; // 문의 개수

	Car() { // 생성자
	}

	Car(String c, String g, int d) { //생성자
		color = c;
		gearType = g;
		door = d;
	}
}

class CarTest {
	public static void main(String[] args) {
		Car c1 = new Car();
		c1.color = "white";
		c1.gearType = "auto";
		c1.door = 4;

		Car c2 = new Car("white", "auto", 4);
	}
}
```

c1 보다 c2 코드가 **더 간결하고 직관적이다.**

이처럼 다양한 생성자를 제공함으로써 인스턴스 생성 후에 별도로 초기화를 하지 않아도 되도록 하는 것이 바람직하다.

# 생성자에서 다른 생성자 호출하기 - this(), this

생성자 간에도 서로 호출이 가능하다. 단, 다음의 **두 조건**을 만족시켜야 한다.

1. 생성자의 이름으로 클래스이름 대신 **this**를 사용한다.
2. 한 생성자에서 다른 생성자를 호출할 때는 반드시 **첫 줄에서만 호출**이 가능하다.

```java
class Car {
	String color;
	String gearType;
	int door;

	Car() { // Car(String color, String gearType, int door)를 호출
		this("white", "auto", 4);
	}

	Car(String color) {
		this(color, "auto", 4);
	}

	Car(String color, String gearType, int door) {
		this.color = color;
		this.gearType = gearType;
		this.door = door;
	}
}

```

## this

인스턴스 자신을 가리키는 **참조변수**, 인스턴스의 주소가 저장되어 있다.

모든 인스턴스메서드에 지역변수로 숨겨진 채로 존재한다.

## this(), this(매개변수)

**생성자**, 같은 클래스의 다른 생성자를 호출할 때 사용한다.

# 생성자를 이용한 인스턴스의 복사

현재 사용하고 있는 인스턴스와 **같은 상태**를 갖는 인스턴스를 하나 더 만들고자 할 때 **생성자**를 이용할 수 있다. 인스턴스의 차이는 인스턴스마다 각기 다른 값을 가질 수 있는 **인스턴스변수** 뿐이다.

```java
class Car {
	String color;
	String gearType;
	int door;

	Car() {
		this("white", "auto", 4);
	}

	Car(Car c) { // 인스턴스의 복사를 위한 생성자
		/*
		c.color = color;
		c.gearType = gearType;
		c.door = door;
		*/
		// 아래와 같이 다른 생성자를 호출하는 것이 바람직하다.
		this(c.color, c.gearType, c.door);
	}

	Car(String color, String gearType, int door) {
		this.color = color;
		this.gearType = gearType;
		this.door = door;
	}
}

class CarTest {
	public static void main(String[] args) {
		Car c1 = new Car();
		Car c2 = new Car(c1); // c1의 복사본 c2를 생성한다.
	}
}
```

# 출처

자바의 정석
