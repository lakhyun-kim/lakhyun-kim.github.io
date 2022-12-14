---
title: 변수의 초기화
author: lakhyun.kim
categories: [Java]
tags: [Java, 변수의 초기화]
pin: false
---

# 변수의 초기화

변수를 선언하고 처음으로 값을 저장하는 것을 **변수의 초기화**라고 한다.

```java
class InitTest {
	int x;      // 인스턴스 변수
	int y = x;  // 인스턴스 변수

	void method1() {
		int i;      // 지역변수
		int j = i;  // 에러. 지역변수를 초기화하지 않고 사용
	}
}
```

**맴버변수(클래스변수와 인스턴스변수)와 배열**의 초기화는 선택적이지만, **지역변수**의 초기화는 필수적이다.

## 맴버변수의 초기화 방법

1. 명시적 초기화
2. 생성자
3. 초기화 블럭
  - 인스턴스 초기화 블럭 : 인스턴스변수를 초기화 하는데 사용.
  - 클래스 초기화 블럭 : 클래스변수를 초기화 하는데 사용.

# 명시적 초기화(explicit initialization)

변수를 선언과 동시에 초기화하는 것을 **명시적 초기화**라고 한다.

여러 초기화 방법 중에서 **가장 우선적**으로 고려되어야 한다.

```java
class Car {
	int door = 4;             // 기본형(primitive type) 변수의 초기화
	Engine e = new Engine();  // 참조형(reference type) 변수의 초기화
}
```

보다 복잡한 초기화 작업이 필요할 때는 **초기화 블럭** 또는 **생성자**를 사용해야 한다.

# 초기화 블럭(initialization block)

초기화 블럭에는 두 가지 종류가 있다.

1. 클래스 초기화 블럭 : 클래스변수의 복잡한 초기화에 사용된다.
2. 인스턴스 초기화 블럭 : 인스턴스변수의 복잡한 초기화에 사용된다.

```java
class InitBlock {
	static { // 클래스 초기화 블럭
	}

	{ // 인스턴스 초기화 블럭
	}
}
```

**클래스 초기화 블럭**은 클래스가 메모리에 처음 로딩될 때 **한번만 수행**되며, **인스턴스 초기화 블럭**은 생성자와 같이 **인스턴스를 생성할 때 마다** 수행된다.

**생성자**보다 **인스턴스 초기화 블럭**이 먼저 수행된다.

```java
class StaticBlockTest {
	static int[] arr = new int[10]; // 명시적 초기화를 통해 배열 arr 생성

	static { // 클래스 초기화 블럭
		for(int i = 0; i < arr.length; i++) {
			// 1과 10사이의 임의의 값을 배열 arr에 저장한다.
			arr[i] = (int)(Math.random() * 10) + 1;
		}
	}

	public static void main(String[] args) {
		for(int i = 0; i < arr.length; i++) {
			// 1과 10사이의 임의의 값이 출력된다.
			System.out.println("arr[" + i + "] : " + arr[i]);
		}
	}
}
```

이처럼 배열이나 예외처리가 필요한 초기화에서는 명시적 초기화만으로는 복잡한 초기화 작업을 할 수 없다. 이런 경우에 추가적으로 **클래스 초기화 블럭**을 사용하도록 한다.

인스턴스변수의 복잡한 초기화는 **생성자** 또는 **인스턴스 초기화 블럭**을 사용한다.

# 맴버변수의 초기화 시기와 순서

**클래스변수의 초기화시점 :** 클래스가 처음 로딩될 때 단 한번 초기화 된다.

**인스턴스변수의 초기화시점 :** 인스턴스가 생성될 때마다 각 인스턴스별로 초기화가 이루어진다.

**클래스변수의 초기화순서 :** 기본값 → 명시적 초기화 → 클래스 초기화 블럭

**인스턴스변수의 초기화순서 :** 기본값 → 명시적 초기화 → 인스턴스 초기화 블럭 → 생성자

```java
class InitTest {
	static int cv = 1; // 명시적 초기화
	       int iv = 1; // 명시적 초기화

	static { // 클래스 초기화 블럭
		cv = 2;
	}

	{ // 인스턴스 초기화 블럭
		iv = 2;
	}

	InitTest() { // 생성자
		iv = 3;
	}
}
```

**클래스변수 초기화** : 클래스가 처음 메모리에 로딩될 때 차례대로 수행된다.

**인스턴스변수 초기화** : 인스턴스를 생성할 때 차례대로 수행된다.

**클래스변수**는 **인스턴스변수**보다 항상 먼저 생성되고 초기화 된다.

# 출처

자바의 정석
