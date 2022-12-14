---
title: 객체지향언어
author: lakhyun.kim
categories: [Java]
tags: [Java, 객체지향언어]
pin: false
---

# **객체지향언어의 역사**

컴퓨터의 초창기에는 주로 **과학실험**이나 **미사일 발사실험**과 같은 모의실험을 목적으로 사용되었다.

이 시절의 과학자들은 모의실험을 위해 실제 세계와 유사한 **가상 세계**를 컴퓨터 속에 구현하고자 노력했고 이러한 노력은 **객체지향이론**을 탄생시켰다.

1960년대 중반에 **시뮬라**라는 최초의 객체지향언어가 탄생하였다.

1980년대 중반에 **C++** 등 여러 객체지향언어가 발표되면서 개발자들의 관심을 끌기 시작했지만 사용자층이 넓지 못했다.

요구사항이 빠르게 변화해가는 상황을 절차적 언어로는 극복하기 어렵다는 한계를 느끼고 객체지향언어를 이용한 개발방법론이 대안으로 떠오르게 되었다.

**자바**가 1995년 발표되고 1990년대 말에 **인터넷의 발전**과 함께 크게 유행하면서 **객체지향언어**는 프로그래밍언어의 주류로 자리잡게 되었다.

# 객체지향언어

프로그램을 다수의 객체로 만들고, 객체끼리 서로 상호작용하도록 관계를 만드는 프로그래밍 언어

## 특징

1. **캡슐화**

   데이터와 코드의 형태를 외부로부터 알 수 없게 하고, 데이터의 구조와 역할, 기능을 하나의 캡슐 형태로 만드는 방법이다. **(정보 은닉)**

   ex) VO에 private 을 붙이고 getter, setter를 만든다.

2. **상속**

   부모클래스에 정의된 변수 및 메서드를 자식 클래스에서 **그대로 이어 받아** 사용하는 것이다.

3. **다형성**

   상속과 연관된 개념, 하나의 객체가 여러 객체로 재구성 되는 것이다. **(오버로딩, 오버라이딩)**

4. **추상화**

   공통의 속성이나 기능을 묶어 이름을 붙이는 것, 객체지향관점에서는 **클래스를 정의**하는 것.


## 장점

1. 코드의 **재사용성**이 높다. **(재사용성)**

   새로운 코드를 작성할 때 기존의 코드를 이용하여 쉽게 작성할 수 있다.

2. 코드의 **관리가 용이**하다. **(유지보수)**

   코드간의 관계를 이용해서 적은 노력으로 쉽게 코드를 변경할 수 있다.

3. **신뢰성 높은 프로그래밍**을 가능하게 한다. **(중복된 코드의 제거)**

   코드의 중복을 제거하여 코드의 불일치로 인한 오동작을 방지할 수 있다.


## 단점

1. **느린 개발 속도**

   정확한 이해가 필요하기에 설계단계부터 많은 시간이 소모된다.

2. **느린 실행 속도**

   컴퓨터가 이해하는데 시간이 걸려 실행속도가 느리다.


# 출처

자바의정석

[https://xangmin.tistory.com/152](https://xangmin.tistory.com/152)

[https://velog.io/@jacobhboy/자바-10.-객체지향언어](https://velog.io/@jacobhboy/%EC%9E%90%EB%B0%94-10.-%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5%EC%96%B8%EC%96%B4)
