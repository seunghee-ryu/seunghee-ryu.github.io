---
layout: post
title:  "Object Class"
categories: TLI
layout : single
---

# 2020-08-13 TLI

## 추상화
- 액터가 앱을 사용해서 컴퓨터를 조작해 업무를 하려면 업무에 필요한 데이터를 정의해야 한다. 이렇게 데이터와 업무 행위를 클래스로 정의하는 것을 추상화라고 한다.
    - 액터라는 것은 동작을 촉발하는 시발점을 이야기한다.
    - 사람, 시스템, 타이머(자동으로 프로그램을 시작시키는 기능)가 액터가 될 수 있다.
    - 업무 데이터는 사람, 사물, 개념에 관한 것들이 있다.
- 데이터를 정의할 때 각 클래스에서 동일하게 쓰이는 변수가 있다면 그것은 상위 클래스를 만들어 상속 받으면 변수를 쉽게 다룰 수 있다.

## Object 클래스의 주요 메서드
- 1) toString() : 클래스 이름과 해시 코드를 리턴한다.
- 2) equals() : 같은 인스턴스인지 검사한다.
- 3) hashCode() : 인스턴스를 식별하는 값을 리턴한다.
- 4) getClass() : 인스턴스의 클래스 정보를 리턴한다.
- 5) clone() : 인스턴스를 복제한 후 그 복제 인스턴스를 리턴한다.
- 6) finalize() : 가비지 컬렉터에 의해 메모리에서 해제되기 직전에 호출된다.
- 위 메서드들은 전부 Object에서 상속받은 메서드들이다.

## Object class
- 자바의 최상위 클래스
    - 클래스를 정의할 때 수퍼 클래스를 지정하지 않으면 컴파일러는 자동으로 오브젝트를 상속받는다.
    - instanceof 연산자를 사용하면 해당 인스턴스가 오브젝트 타입인지 확인할 수 있다.
    - instanceof 연산자는 레퍼런스가 가리키는 인스턴스가 지정한 클래스의 인스턴스이거나 조상으로 가지는지 검사한다.
    - 자바의 모든 클래스는 오브젝트의 자손이다.

## 해시값 = 인스턴스 식별자
 - 인스턴스마다 부여된 고유의 식별자.
    - 인스턴스의 주소가 아니다
    - 인스턴스가 같은지 아닌지 검사할 때 사용할 수 있다.
    - hashCode()를 재정의하지 않고 원래 메서드를 그대로 사용하면 무조건 인스턴스마다 새 해시값이 부여된다.

## toString() 메서드
- 클래스 정보를 간단히 출력한다.
- println()에 넘겨주는 값이 String 값이 아니라면 toString()을 호출한 후 그 값을 리턴한다.
    - 따라서 System.out.println(obj.toString()); 는 System.out.println(obj); 와 같다
    - toString()을 호출하면 "패키지 이름을 포함한 클래스명@인스턴스 식별자" 형식의 문자열을 리턴한다.
    - 패키지명.클래스명@16진수해시코드
- toString()을 오버라이딩 할 때.
    - 인스턴스의 현재 값을 간단히 확인하고 싶을 때 toString()을 오버라이딩 한다.
- toString()은 수퍼 클래스인 Object의 메서드이다.
    - 따라서 클래스를 정의할 때 수퍼 클래스를 지정하지 않으면 자동으로 java.lang.Object 클래스가 수퍼 클래스로 지정된다.
    - 그래서 자바의 모든 클래스는 toString()을 호출할 수 있다. 즉 자바의 모든 클래스는 Object 클래스에 정의된 메서드를 호출할 수 있다.
- Object로부터 상속받은 toString()의 리턴 값이 마음에 들지 않는다면 재정의(오버라이딩) 하면 된다.

## equals() 메서드
- Object에서 상속 받은 equals()는 == 연산자와 마찬가지로 인스턴스가 같은지를 비교한다.
    - 만약 그 내용물이 같은지 비교하고 싶다면 equals()를 재정의(오버라이딩) 해야한다.
- String 과 Wrapper 클래스는 자체적으로 equals()를 오버라이딩해서 인스턴스의 데이터가 같은지 비교한다.
    - String 클래스는 toString()을 오버라이딩 해서 인스턴스가 다르더라도 문자열이 같으면 true를 리턴하도록 메서드를 재정의 했기 때문에(같은 해시값을 출력하도록 되어있다) String에 대해서 equals()를 호출하면 true를 리턴한다.

## hashCode() 메서드
- Object에서 상속받은 hashCode()는 인스턴스마다 고유의 4바이트 정수값을 리턴한다.
    - 이 값은 toString()의 출력 값으로 사용된다.
- String 클래스의 hashCode() 메서드는 같은 문자열에 대해 같은 해시값을 리턴한다.
- 두 개의 인스턴스가 같은 데이터인지를 비교하기 위해선 hashCode()를 재정의(오버라이딩) 할 필요가 있다.
    - 보통 equals()와 같이 사용되기 때문에 함께 오버라이딩 된다.
    - 재정의하는 가장 간단한 방법은 모든 값을 문자열로 만틀어 붙인 다음에 String 클래스에 있는 hashCode()를 사용하는 것이다. 왜냐하면 String 클래스에 있는 hashCode()는 문자열이 같은 경우 같은 해시값을 리턴하도록 이미 오버라이딩 되어 있기 때문이다.

## HashSet과 hashCode()
- HashSet
    - 집합의 기능을 수행한다. 중복 값을 저장하지 않는다.
    - 저장할 객체에 대해 hash 코드로 중복 여부를 검사한다.
    - 해시값이 다르면 다른 값으로 취급한다.
    - 또한 hash 코드로 값을 저장할 인덱스를 결정하기 때문에 값을 꺼낼 때 저장한 순서대로 꺼낼 수 없다.
    - hashCode()와 equals()를 오버라이딩 하여 같은 데이터에 대해 같은 해시 코드를 리턴하도록 만들면 중복 값을 저장하지 않게 된다.
        - hashCode()는 같은 필드 값을 갖는 경우 같은 해시 코드를 리턴하도록 변경하고
        - equals()는 필드 값이 같을 경우 true를 리턴하도록 변경한다.

## HashMap의 key와 hashCode()
- 값을 저장할 때 key 객체의 해시 코드를 이용하여 저장할 위치(인덱스)를 계산한다. 따라서 해시 코드가 같다면 같은 key로 간주한다.
- hashCode() 와 equals()를 오버라이딩 해서 같은 해시 코드를 가지게 만들고 equals()도 인스턴스가 아닌 값을 비교하게 만들면 내용이 같은 각각의 key 객체를 같은 key로 사용할 수 있다.
- key 실행원리
    - key 파라미터로 받은 객체에 대해 hashCode()를 호출하여 정수값을 얻는다. 그리고 이 정수값을 이용하여 값이 저장된 위치를 찾는다.
    - 원래의 키와 같은지 equals()로 한번 더 비교한다. 만약 같다면 같은 키로 간주하여 해당 값을 꺼내 리턴한다.
    - Integer 클래스 등의 Wrapper 클래스와 String 클래스는 Object 클래스에서 상속받은 hashCode()와 equals()를 오버라이딩 했기 때문에 인스턴스가 다르더라도 인스턴스 필드의 값이 같으면 hashCode()의 리턴값이 같고 equals()가 true를 리턴한다.

## getClass() 메서드
- 해당 클래스의 정보를 리턴한다.
- 레퍼런스를 통해서 인스턴스의 클래스 정보를 알아낼 수 있고, 클래스 정보로부터 다양한 값을 꺼낼 수 있다.
- 값을 한 번 밖에 사용하지 않을 것이라면 체인 방식으로 호출하는 것이 편하다.

## clone() 메서드
- 인스턴스를 복제할 때 호출하는 메서드이다.
- Object에서 상속받은 clone()은 protected이다. 따라서 같은 패키지에 소속된 클래스이거나 상속받은 서브 클래스가 아니면 호출할 수 없다.
    - 이 문제를 해결하기 위해서 Object에서 상속받은 clone()을 오버라이딩 해야한다. 다른 패키지의 멤버가 호출하려면 public으로 접근 제어의 범위를 넓히면 된다. 리턴 타입은 해당 클래스의 이름으로 변경한다.
- 복제 대상이 되는 클래스에서 clone() 메서드의 사용을 활성화 시키기 위해 Cloneable 인터페이스를 활성화 시켜야 한다.
    - JVM에게 클래스의 인스턴스를 복제할 수 있음을 표시한다.
- shallow copy vs deep copy
    - Object의 clone()은 해당 객체의 필드 값만 복제하고 그 인스턴스 변수가 가리키고 있는 객체는 복제하지 않는다. 이것을 shallow copy라고 한다.
    - 객체의 인스턴스 변수가 가리키고 있는 객체까지 복제하는 것을 deep copy라고 한다. deep copy는 개발자가 직접 clone() 메서드 안에 deep copy를 수행하는 코드를 작성해야 한다.