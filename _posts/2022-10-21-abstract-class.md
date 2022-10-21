---
title: 추상클래스(abstract class)
author: lakhyun.kim
categories: [Java]
tags: [Java, 추상클래스, abstract class]
pin: false
---

# 추상클래스란?

클래스를 설계도에 비유한다면, 추상클래스는 **미완성 설계도**에 비유할 수 있다.

클래스가 미완성이라는 것은 맴버의 개수에 관계된 것이 아니라, 단지 **미완성 메서드(추상메서드)를** 포함하고 있다는 의미이다.

미완성 설계도로 완성된 제품을 만들 수 없듯이 **추상클래스로 인스턴스는 생성할 수 없다. 추상클래스는 상속을 통해서 자손클래스에 의해서만 완성될 수 있다.**

추상클래스는 **키워드 abstract**를 붙이기만 하면 된다.

```java
abstract class 클래스이름 {
	// ...
}
```

추상클래스는 추상메서드를 포함하고 있다는 것을 제외하고는 일반클래스와 전혀 다르지 않다. 추상클래스에도 생성자가 있으며, 맴버변수와 메서드도 가질 수 있다.

# 추상메서드(abstract method)

메서드의 선언부만 작성하고 구현부는 작성하지 않은 채로 남겨 둔 것이 **추상메서드**이다. 즉, 설계만 해 놓고 실제 수행될 내용은 작성하지 않았기 때문에 **미완성 메서드**인 것이다.

추상메서드 역시 **키워드 abstract**를 앞에 붙여 주고, 추상메서드는 구현부가 없으므로 괄호{}대신 문장의 끝을 알리는 ;를 적어준다.

```java
/* 주석을 통해 어떤 기능을 수행할 목적으로 작성하였는지 설명한다. */
abstract 리턴타입 메서드이름();
```

추상클래스로부터 상속받는 자손클래스는 오버라이딩을 통해 조상인 추상클래스의 추상메서드를 모두 구현해주어야 한다. **만일 조상으로부터 상속받은 추상메서드 중 하나라도 구현하지 않는다면, 자손클래스 역시 추상클래스로 지정해 주어야 한다.**

```java
abstract class Player { // 추상클래스
	abstract void play(int pos);       // 추상메서드
	abstract void stop();              // 추상메서드
}

class AudioPlayer extends Player {
	void play(int pos) { /* 내용 생략 */ }    // 추상메서드를 구현
	void stop() { /* 내용 생략 */ }           // 추상메서드를 구현
}

abstract class AbstractPlayer extends Player {
	void play(int pos) { /* 내용 생략 */ }    // 추상메서드를 구현
}
```

# 추상클래스의 작성

**추상화**는 기존의 클래스의 **공통부분**을 뽑아내서 조상클래스를 만드는 것이라고 할 수 있다.

추상화 - 클래스간의 공통점을 찾아내서 **공통의 조상**을 만드는 작업

구체화 - 상속을 통해 클래스를 **구현, 확장**하는 작업

```java
class Marine {    // 보병
	int x, y;       // 현재 위치
	void move(int x, int y) { /* 지정된 위치로 이동 */ }
	void stop()             { /* 현재 위치에 정지 */ }
	void stimPack()         { /* 스팀팩을 사용한다. */ }
}

class Tank {      // 탱크
	int x, y;       // 현재 위치
	void move(int x, int y) { /* 지정된 위치로 이동 */ }
	void stop()             { /* 현재 위치에 정지 */ }
	void changeMode()       { /* 공격모드로 변환한다. */ }
}

class Dropship {  // 수송선
	int x, y;       // 현재 위치
	void move(int x, int y) { /* 지정된 위치로 이동 */ }
	void stop()             { /* 현재 위치에 정지 */ }
	void load()             { /* 선택된 대상을 태운다. */ }
	void unload()           { /* 선택된 대상을 내린다. */ }
}
```

위에 클래스로부터 공통된 부분을 뽑아내어 추상클래스를 만들어보면 아래와 같다.

```java
abstract class Unit {
	int x, y;       // 현재 위치
	abstract void move(int x, int y);
	void stop() { /* 현재 위치에 정지 */ }
}

class Marine extends Unit {    // 보병
	void move(int x, int y) { /* 지정된 위치로 이동 */ }
	void stimPack()         { /* 스팀팩을 사용한다. */ }
}

class Tank extends Unit {      // 탱크
	void move(int x, int y) { /* 지정된 위치로 이동 */ }
	void changeMode()       { /* 공격모드로 변환한다. */ }
}

class Dropship extends Unit {  // 수송선
	void move(int x, int y) { /* 지정된 위치로 이동 */ }
	void load()             { /* 선택된 대상을 태운다. */ }
	void unload()           { /* 선택된 대상을 내린다. */ }
}
```

이 Unit클래스는 다른 유닛을 위한 클래스를 작성하는데 **재활용**될 수 있을 것이다.

# 출처

자바의 정석
