---
title: 오버라이딩(overriding)
author: lakhyun.kim
categories: [Java]
tags: [Java, 오버라이딩, overriding]
pin: false
---

# 오버라이딩이란?

조상 클래스로부터 **상속**받은 메서드의 내용을 **변경**하는 것이다. 상속받은 메서드를 그대로 사용하기도 하지만, 자손 클래스에 맞게 변경해야하는 경우 **오버라이딩**한다.

```java
class Point {
	int x;
	int y;

	String getLocation() {
		return "x :" + x + ", y :" + y;
	}
}

class Point3D extends Point {
	int z;

	String getLocation() { // 오버라이딩
		return "x :" + x + ", y :" + y + ", z :" + z;
	}
}
```

# 오버라이딩의 조건

자손 클래스에서 오버라이딩하는 메서드는 조상 클래스의 메서드와 **선언부**가 같아야 한다.

- **이름**이 같아야 한다.
- **매개변수**가 같아야 한다.
- **반환타입**이 같아야 한다.

다만 **접근 제어자**와 **예외**는 제한된 조건 하에서만 다르게 변경할 수 있다.

1. 접근 제어자는 조상 클래스의 메서드보다 **좁은 범위**로 변경할 수 없다.
   ex) 조상 클래스에 정의된 메서드의 접근 제어자가 **protected**라면, 이를 **오버라이딩**하는 자손 클래스의 메서드는 접근 제어자가 **protected**나 **public**이어야 한다.

   **넓은 것에서 좁은 것 순으로 나열 :** public, protected, (default), private

2. 조상 클래스의 메서드보다 **많은 수의 예외**를 선언할 수 없다.

    ```java
    class Parent {
    	void parentMethod() throws IOException, SQLException {
    		// ...
    	}
    }

    class Child extends Parent {
    	void parentMethod() throws IOException { // 예외의 개수가 적으므로 가능
    		// ...
    	}
    }

    class Child2 extends Parent {
    	void parentMethod() throws Exception { // 예외의 개수가 적지만 Exception은 모든 예외의 최고 조상이므로 불가능
    		// ...
    	}
    }
    ```

3. 인스턴스메서드를 **static메서드**로 또는 그 반대로 변경할 수 없다.

   static메서드를 똑같은 이름의 static메서드로 정의할 수 있지만 이것은 각 클래스에 **별개의 static메서드**를 정의한 것일 뿐 **오버라이딩**이 아니다.


# 오버로딩 vs. 오버라이딩

**오버로딩(overloading)**   기존에 없는 새로운 메서드를 정의하는 것(**new**)

**오버라이딩(overriding)**   상속받은 메서드의 내용을 변경하는 것(**change**, **modify**)

```java
class Parent {
	void parentMethod() {}
}

class Child extends Parent {
	void parentMethod() {}       // 오버라이딩
	void parentMethod(int i) {}  // 오버로딩

	void childMethod() {}
	void childMethod(int i) {}   // 오버로딩
	void childMethod() {}        // 에러. 중복정의 되었음
}
```

# super

자손 클래스에서 조상 클래스로부터 **상속받은 맴버를 참조**하는데 사용되는 참조변수이다. 맴버변수와 지역변수의 이름이 같을 때 **this**를 사용해서 구별했듯이 상속받은 맴버와 자신의 클래스에 정의된 맴버의 이름이 같을 때는 **super**를 사용해서 구별할 수 있다.

```java
class SuperTest {
	public static void main(String[] args) {
		Child c = new Child();
		c.method();
	}
}

class Parent {
	int x = 10;
}

class Child extends Parent {
	void method() {
		System.out.println("x = " + x);
		System.out.println("this.x = " + this.x);
		System.out.println("super.x = " + super.x);
	}
}

/*
[실행결과]
x = 10
this.x = 10
super.x = 10
*/
```

이 경우 x, this.x, super.x 모두 같은 변수를 의미한다.

```java
class SuperTest2 {
	public static void main(String[] args) {
		Child c = new Child();
		c.method();
	}
}

class Parent {
	int x = 10;
}

class Child extends Parent {
	int x = 20;

	void method() {
		System.out.println("x = " + x);
		System.out.println("this.x = " + this.x);
		System.out.println("super.x = " + super.x);
	}
}

/*
[실행결과]
x = 20
this.x = 20
super.x = 10
*/
```

**같은 이름의 맴버변수**가 조상 클래스에 있고 자손 클래스에도 있을 때는 super.x와 this.x는 서로 다른 값을 참조하게 된다.

# super() - 조상 클래스의 생성자

this()와 마찬가지로 super() 역시 **생성자**이다. **this()는** 같은 클래스의 다른 생성자를 호출하는데 사용되지만, **super()는** 조상 클래스의 생성자를 호출하는데 사용된다.

Object클래스를 제외한 모든 클래스의 생성자 첫 줄에는 **생성자, this()** 또는 **super()를** 호출해야 한다. 그렇지 않으면 컴파일러가 자동적으로 **super();를** 생성자의 첫 줄에 삽입한다.

```java
class PointTest {
	public static void main(String[] args) {
		Point3D p3 = new Point3D(1, 2, 3);
	}
}

class Point {
	int x;
	int y;

	Point(int x, int y) {
		this.x = x;
		this.y = y;
	}

	String getLocation() {
		return "x : " + x + ", y : " + y;
	}
}

class Point3D extends Point {
	int z;

	Point3D(int x, int y, int z) {
		// 생성자 첫 줄에 다른 생성자를 호출하지 않기 때문에 컴파일러가 'super();'를 여기에 삽입한다.
		// super()는 Point3D의 조상인 Point클래스의 기본 생성자인 Point()를 의미한다.
		// 하지만 조상 클래스의 Point()가 없기 때문에 컴파일에러가 발생할 것이다.
		this.x = x;
		this.y = y;
		this.z = z;
	}

	String getLocation() { // 오버라이딩
		return "x : " + x + ", y : " + y + ", z : " + z;
	}

}
```

아래처럼 변경하면 문제없이 컴파일 될 것이다.

```java
Point3D(int x, int y, int z) {
	super(x, y);  // 조상클래스의 생성자 Point(int x, int y)를 호출한다.
	this.z = z;
}

```

# 출처

자바의 정석
