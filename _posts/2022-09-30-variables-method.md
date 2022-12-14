---
title: 변수와 메서드
author: lakhyun.kim
categories: [Java]
tags: [Java, 변수, 메서드]
pin: false
---

# 선언위치에 따른 변수의 종류

변수는 **클래스변수, 인스턴스변수, 지역변수**가 있다.

변수의 종류를 결정짓는 중요한 요소는 **‘변수의 선언된 위치’** 다.

맴버변수를 제외한 나머지 변수들은 모두 **지역변수**이며, 맴버변수 중 static이 붙는 것은 **클래스변수**, 붙지 않는 것은 **인스턴스변수**이다.

```java
class Variables {
	// 클래스영역
	int iv;          // 인스턴스변수
	static int cv;   // 클래스변수(static변수, 공유변수)

	void method() {
		// 메서드영역
		int lv = 0;    // 지역변수
	}
}
```

## 변수의 종류와 특징

| 변수의 종류 | 선언위치 | 생성시기 |
| --- | --- | --- |
| 클래스변수 | 클래스영역 | 클래스가 메모리에 올라갈 때 |
| 인스턴스변수 | 클래스영역 | 인스턴스가 생성되었을 때 |
| 지역변수 | 클래스영역 이외의 영역
(메서드, 생성자, 초기화 블럭 내부) | 변수 선언문이 수행되었을 때 |

## 인스턴스변수(instance variable)

클래스의 **인스턴스를 생성**할 때 만들어진다. 그렇기 때문에 인스턴스 변수의 값을 읽어 오거나 저장하기 위해서는 먼저 인스턴스를 생성해야한다. 인스턴스는 서로 다른 값을 가질 수 있어서 인스턴스마다 고유한 상태를 유지해야하는 경우, 인스턴스변수로 선언한다.

## 클래스변수(class variable)

인스턴스변수 앞에 **static**을 붙이기만 하면 된다. 인스턴스변수와는 달리 모든 인스턴스가 공통된 저장공간(변수)을 공유하게 된다. 한 클래스의 모든 인스턴스들이 공통적인 값을 유지해야하는 경우, 클래스변수로 선언한다.

인스턴스를 생성하지 않고도 ‘**클래스이름.클래스변수**’와 같은 형식으로 바로 사용할 수 있다. 클래스가 메모리에 ’**로딩**’될 때 생성되어 프로그램이 종료될 때 까지 유지되며, **public**을 앞에 붙이면 어디서나 접근할 수 있는 ’**전역변수**’가 된다.

## 지역변수(local variable)

메서드 내에 선언되어 메서드 내에서만 사용 가능하며, 메서드가 종료되면 소멸되어 사용할 수 없게 된다.

# 클래스변수와 인스턴스변수

**인스턴스변수**는 인스턴스가 생성될 때 마다 생성되므로 인스턴스마다 **각기 다른 값**을 유지할 수 있지만, **클래스변수**는 모든 인스턴스가 하나의 저장공간을 공유하므로 **항상 공통된 값**을 갖는다.

# 메서드

특정 작업을 수행하는 **문장들을 하나로 묶은 것**이다.

메서드에 넣을 값(**입력**)과 반환하는 결과(**출력**)만 알면 된다.

## 메서드를 사용하는 이유

1. 높은 재사용성

   한번 만들어 놓은 메서드는 몇 번이고 호출할 수 있다.

2. 중복된 코드의 제거

   반복되는 문장들을 묶어서 하나의 메서드로 작성한다.

3. 프로그램의 구조화

   문장들을 작업단위로 나눠서 여러 개의 메서드에 담아 프로그램의 구조를 단순화시키는 것이 필수적이다.


# 메서드의 선언과 구현

선언부와 구현부로 이루어져 있다.

```java
반환타입 메서드이름 (매개변수1, 매개변수2, ...) { // 선언부
	// 구현부
	// 메서드 호출 시 수행될 코드
}
```

## 메서드 선언부

반환타입(출력), 메서드이름, 매개변수 선언(입력)으로 구성되어 있다.

### 매개변수 선언

메서드가 작업을 수행하는데 필요한 값들(**입력**)을 제공받기 위한 것이다. 매개변수도 **지역변수**다.

### 메서드이름

이름만으로도 메서드의 기능을 쉽게 알 수 있도록 **함축적**이면서도 **의미있는 이름**을 짓도록 노력해야 한다.

### 반환타입

메서드의 작업수행 결과(**출력**)인 반환값의 타입을 적는다. 반환값이 없는 경우 **‘void’** 를 적어야 한다.

## 메서드의 구현부

메서드를 호출했을 때 수행될 문장들을 넣는다.

### return문

메서드의 반환타입이 ‘void’가 아닌 경우, 구현부{}안에 ‘return 반환값;’이 반드시 포함되어 있어야 한다.

### 지역변수

지역변수는 메서드 내의 선언된 변수이고, 그 메서드 내에서만 사용할 수 있다.

# 메서드의 호출

메서드를 호출해야만 구현부{}의 문장들이 수행된다.

```java
메서드이름(값1, 값2, ...) // 메서드 호출 방법
```

## 인자와 매개변수

메서드를 호출할 때 괄호안에 넣는 값을 **인자** 또는 **인수**라고 한다.

```java
int result = add(3, 5); // 3, 5 인자

int add(int x, int y) { // x, y 매개변수
	int result = x + y;
	return result;
}
```

# return문

현재 실행중인 메서드를 종료하고 호출한 메서드로 되돌아간다.

void 인 경우 컴파일러가 자동으로 return; 을 추가해준다.

# JVM의 메모리구조

응용프로그램이 실행되면, JVM은 시스템으로부터 프로그램을 수행하는데 필요한 메모리를 할당받고 JVM은 이 메모리를 용도에 따라 **method area, call stack, heap 영역**으로 나누어 관리한다.

## 메서드영역(method area)

어떤 클래스가 사용되면, JVM은 해당 클래스의 클래스파일을 읽어서 클래스에 대한 정보(**클래스 데이터, 클래스변수**)를 이곳에 저장한다.

## 힙(heap)

**인스턴스**는 모두 이곳에 생성된다. 즉, **인스턴스변수**들이 생성되는 공간이다.

## 호출스택(call stack 또는 execution stack)

메서드가 호출되면 수행에 필요한 만큼의 메모리를 스택에 할당받는다.

메서드가 수행을 마치고나면 사용했던 메모리를 반환하고 스택에서 제거된다.

호출스택의 제일 위에 있는 메서드가 현재 실행중인 메서드이다.

아래에 있는 메서드가 바로 위의 메서드를 호출한 메서드이다.

```java
class CallStackTest2 {
	public static void main(String[] args) {
		System.out.println("main(String[] args)이 시작되었음.");
		firstMethod();
		System.out.println("main(String[] args)이 끝났음.");
	}

	static void firstMethod() {
		System.out.println("firstMethod()이 시작되었음.");
		secondMethod();
		System.out.println("firstMethod()이 끝났음.");
	}

	static void secondMethod() {
		System.out.println("secondMethod()이 시작되었음.");
		System.out.println("secondMethod()이 끝났음.");
	}
}

[실행결과]
main(String[] args)이 시작되었음.
firstMethod()이 시작되었음.
secondMethod()이 시작되었음.
secondMethod()이 끝났음.
firstMethod()이 끝났음.
main(String[] args)이 끝났음.
```

# 기본형 매개변수와 참조형 매개변수

기본형 매개변수 - 변수의 값을 읽기만 할 수 있다. **(read only)**  ex) int, boolean 등

참조형 매개변수 - 변수의 값을 읽고 변경할 수 있다. **(read & write)**  ex) 배열, 객체

# 참조형 반환타입

반환타입이 **‘참조형’** 이라는 것은 메서드가 ’**객체의 주소**’를 반환한다는 것을 의미한다.

# 재귀호출(recursive call)

메서드의 내부에서 **메서드** **자신을 다시 호출하는 것**이라 하고, 재귀호출을 하는 메서드를 ‘**재귀 메서드**’라 한다.

대부분의 재귀호출은 **반복문**으로 작성하는 것이 가능하지만 재귀호출을 사용하는 이유는 재귀호출이 주는 **논리적 간결함** 때문이다.

재귀호출은 **비효율적**이므로 재귀호출에 드는 비용보다 재귀호출의 간결함이 주는 이득이 충분히 큰 경우에만 사용해야 한다.

# 클래스 메서드(static메서드)와 인스턴스 메서드

변수에서 그랬던 것과 같이, 메서드 앞에 static이 붙어 있으면 **클래스 메서드**이고 붙어 있지 않으면 **인스턴스 메서드**이다.

클래스의 맴버변수 중 모든 인스턴스에 **공통된 값을 유지**해야하는 것이 있는지 살펴보고 있으면, **static**을 붙여준다.

작성한 메서드 중에서 인스턴스 변수나 인스턴스 메서드를 사용하지 않는 메서드에 **static**을 붙일 것을 고려한다.

```java
long add() { return a + b; } // 인스턴스 메서드
static long add(long a, long b) { return a + b; } // 클래스 메서드
```

# 클래스 맴버와 인스턴스 맴버간의 참조와 호출

같은 클래스에 속한 맴버들 간에는 별도의 인스턴스를 생성하지 않고도 서로 참조 또는 호출이 가능하다.

단, 클래스 맴버가 인스턴스 맴버를 참조 또는 호출하고자 하는 경우에는 인스턴스를 생성해야 한다.

그 이유는 인스턴스 맴버가 존재하는 시점에 클래스 맴버는 항상 존재하지만, 클래스 맴버가 존재하는 시점에 인스턴스 맴버가 존재하지 않을 수도 있기 때문이다.

**ex) static 메서드 안에 인스턴스 메서드를 호출할 수 없다. static 메서드는 호출할 수 있다.**

# 출처

자바의 정석
