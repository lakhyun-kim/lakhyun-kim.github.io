---
title: 오버로딩(overloading)
author: lakhyun.kim
categories: [Java]
tags: [Java, 오버로딩, overloading]
pin: false
---

# 오버로딩이란?

한 클래스 내에 같은 이름의 메서드를 여러 개 정의하는 것이다.

# 오버로딩의 조건

1. 메서드 이름이 같아야 한다.
2. 매개변수의 개수 또는 타입이 달라야 한다.

# 오버로딩의 예

가장 대표적인 것은 **println메서드**이다. println메서드를 호출할 때 매개변수로 지정하는 값의 타입에 따라서 호출되는 println메서드가 달라진다.

```java
[보기1] 매개변수의 타입과 개수가 같기 때문에 오버로딩이 성립하지 않는다.
int add(int a, int b) { return a + b; }
int add(int x, int y) { return x + y; }

[보기2] 매개변수의 타입과 개수가 같기 때문에 오버로딩이 성립하지 않는다.
int add(int a, int b) { return a + b; }
long add(int a, int b) { return (long)(a + b); }

[보기3] 매개변수의 순서가 다르기 때문에 오버로딩이 성립한다.
int add(int a, long b) { return a + b; }
long add(long a, int b) { return a + b; }

[보기4] 매개변수의 타입과 개수가 다르기 때문에 오버로딩이 성립한다.
int add(int a, int b) { return a + b; }
long add(long a, long b) { return a + b; }
long add(int[] a) { // 배열의 모든 요소의 합을 반환한다.
	long result = 0;

	for(int i = 0; i < a.length; i++) {
		result += a[i];
	}
	return result;
}
```

**[보기4]** 처럼 같은 일을 하지만 매개변수를 달리해야하는 경우에 **오버로딩**을 구현한다.

# 오버로딩의 장점

하나의 이름으로 정의되므로 기억하기도 쉽고 이름도 짧게 할 수 있어서 오류의 가능성을 많이 줄일 수 있다.

메서드의 이름만 보고도 **이 메서드들은 이름이 같으니, 같은 기능을 하겠구나.** 라고 쉽게 예측할 수 있다.

메서드의 이름을 절약할 수 있다.

# 가변인자(varargs)와 오버로딩

## 가변인자란?

JDK1.5부터 매개변수 개수를 동적으로 지정해 줄 수 있게 되었으며, 이 기능을 **가변인자(variable arguments)** 라고 한다.

**타입… 변수명** 과 같은 형식으로 선언하며, printf()가 대표적인 예이다.

```java
public PrintStream printf(String format, Object... args) { ... }
```

가변인자 외에도 다른 매개변수가 더 있다면 가변인자를 **제일 마지막**에 선언해야 한다.

```java
static String concatenate(String delim, String... args) {
	String result = "";

	for(String str : args) {
		result += str + delim;
	}
	return result;
}

static String concatenate(String... args) {
	return concatenate("", args);
}
```

위에 concatenate메서드처럼 오버로딩하면 컴파일러는 어떤 메소드를 사용 해야하는지 **구분을 못하고** **컴파일 에러**가 난다.

가변인자를 선언한 메서드를 오버로딩하면, 메서드를 호출했을 때 구별되지 못하는 경우가 발생하기 쉽기 때문에 **가능하면 가변인자를 사용한 메서드는 오버로딩하지 않는 것이 좋다.**

# 출처

자바의 정석
