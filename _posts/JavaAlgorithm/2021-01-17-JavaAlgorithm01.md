---
layout: post
title: JavaAlgorithm01
categories: JavaAlgorithm
layout : single
toc : true 
toc_sticky : true
---

# 01 기본 알고리즘

## 01-1 알고리즘이란?

- 알고리즘이란 문제를 해결하기 위한 것으로, 명확하게 정의되고 순서가 있는 유한 개의 규칙으로 이루어진 집합.



### 세 값의 최댓값

```
int max = a;
if (b > max) max = b;
if (c > max) max = c;

- max에 a 값을 넣는다.
- b 값이 max 보다 크면 max에 b 값을 넣는다.
- c 값이  max 보다 크면 max에 c 값을 넣는다.
```

- 세 문장이 아래로 나란히 있다면 이 문장은 순서대로 실행된다.
  - 여러 문장(프로세스)이 순차적으로 실행되는 구조를 순차적 구조라고 한다.
- ()) 안에 있는 식의 평가 결과에 따라 프로그램의 실행 흐름을 변경하는 if문을 선택 구조라고 한다.
- 세 값의 대소 관계의 조합은 13가지 종류가 있다.
  - 조합을 나열한 나무 형태의 모양을 결정 트리라고 한다.
  - 결정 트리는 왼쪽 끝에서 시작하여 오른쪽으로 이동한다.
  - 조건이 성립하면 윗가지로, 성립하지 않으면 아랫가지로 이동한다.



### 세 값의 중앙값

```java
if (a >= b)
  if (b >= c)
    return b;
	else if (a <= C)
    return a;
	else
    return c;
else if (a > c)
  return a;
else if (b > c)
  return c;
else 
  return b;
```



### 조건 판단과 분기

- if - else if - else 는 분기가 3개
```java
if (n > 0)
  System.out.println("이 수는 양수입니다.");
else if (n < 0)
  System.out.println("이 수는 음수입니다.");
else
  System.out.println("이 수는 0입니다.");
```
- if - else if - else if 는 실제로는 분기가 4개

```java
if (n == 1)
  System.out.println("이 수는 1입니다.");
else if (n == 2)
  System.out.println("이 수는 2입니다.");
else if (n == 3)
  System.out.println("이 수는 3입니다.");

// 마지막 else if 의 if (n == 3)를 삭제하면
// 3 이상의 숫자를 입력했을 때도 "이 수는 3입니다."라는 문장이 출력된다.
if (n == 1)
  System.out.println("이 수는 1입니다.");
else if (n == 2)
  System.out.println("이 수는 2입니다.");
else
  System.out.println("이 수는 3입니다.");

// 분기 4개로 변형
if (n == 1)
  System.out.println("이 수는 1입니다.");
else if (n == 2)
  System.out.println("이 수는 2입니다.");
else if (n == 3)
  System.out.println("이 수는 3입니다.");
else
  ; // 공백문(실제로는 아무것도 하지 않는 문장)

```



#### 연산자와 피연산자

- 연산 기호를 연산자라 부른다.
- 연산의 대상이 되는 것을 피연산자라 부른다.

- 연산자는 피연산자의 수에 따라 3종류로 분류된다.
  - 단항 연산자 : 피연산자 1개. 예) a++
  - 2항 연산자 : 피연산자 2개. 예) a < b
  - 3항 연산자 : 피연산자 3개. 예) a ? b : c
- 특히 조건 연산자는 자바에서 유일한 3항 연산자이다.
  - a ? b : c는 a가 참일때 b를 리턴, 거짓일 때 c를 리턴한다.



### 순서도의 기호

- 데이터 : 데이터의 입력과 출력을 나타낸다.
- 처리 : 여러 종류의 처리 기능을 수행한다.
- 미리 정의한 처리 : 다른 곳에서 이미 정의한 하나 이상의 연산 또는 명령어들로 이루어진 처리를 나타낸다.
- 판단 : 하나의 입구와 하나 이상을 선택할 수 있는 출구가 있고, 기호에서 정의한 조건을 평가하여 하나의 출구를 선택하는 판단 기능을 나타낸다.
- 루프 범위 : 루프의 시작과 종료를 나타낸다.
- 선 : 제어의 흐름을 나타낸다.
- 단말 : 외부 환경으로 나가거나 외부 환경에서 드어오는 것을 나타낸다.
- 기호는 책 25p



## 01-2 반복

### 1부터 n 까지의 정수 합 구하기

#### while문 반복

```java
int sum = 0;
int i = 1;

while (i <= n) {
  sum += i;
  i++;
}
```

- 어떤 조건이 성립하는 동안 처리를 반복하여 실행하는 것을 반복 구조라 하며 일반적으로 루프라고 부른다.
- 이때 while 문은 실행 전에 반복을 계속할지 판단하는데 이런 구조를 사전 판단 ㅂ나복 구조라고 부른다.



#### for문 반복

```java
int sum = 0;

for (int i = 1; i <= n; i++)
  sum += i;
```

- for (초기화 부분; 제어식; 업데이트 부분) 명령문
- 초기화 부분은 for문을 실행하기 전에 한번만 실행된다.
- 제어식을 평가한 값이 참이면 for문의 명령문을 반복한다.
- 명령문을 실행한 다음에는 업데이트 부분을 실행한다.



#### do 반복문

```
do {
	n = stdIn.nextInt();
} while (n <= 0);
```

- do 문은 일단 루프 ㅂ노문을 한 번 실행한 다음에 계속 반복할 것인지를 판단하는 사후 판단 반복문이다.



#### 사전 판단 반복과 사후 판단 반복의 차이점

- 사전 판단 반복문은 처음에 제어식을 평가한 결과가 0이면 루프 본문은 한번도 실행되지 않는다.
- 사후 판단 반복문은 루프 본문이 반드시 한번은 실행된다.



### 구조적 프로그래밍

- 하나의 입구와 하나의 출구를 가진 구성 요소만을 계층적으로 배치하여 프로그램을 구성하는 방법을 구조적 프로그래밍이라고 한다.
- 구조적 프로그래밍은 순차, 선택, 반복이라는 3조율의 제어 흐름을 사용한다.



### 다중 루프

- 반복을 루프로 중첩시키는 것

```java
// 이중 루프로 곱셈표를 출력한다.
for (int i = 1, i <= 9; i++) {
	for (int j = 1; j <= 9; j++) {
		System.out.println(i * j);
	}
}
```



### 직각 이등변 삼각형 출력

- 이중 루프를 응용하면 기호를 늘어놓아 삼각형이나 사각형 모양을 출력할 수 있다.

```java
do {
	System.out.print("몇 단 삼각형입니까?: ");
	n = stdIn.nextInt();
} while (n <= 0);

for (int i = 1; i <= n, i++) {
	for (int j = 1; j <= i; j++) 
		System.out.print('*');
}

// 숫자 5를 입력했을 경우
// *
// **
// ***
// ****
// *****
// 가 출력된다.
```
