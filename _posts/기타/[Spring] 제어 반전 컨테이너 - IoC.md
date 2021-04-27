---
ayout: post
title: 제이 반전 컨테이너
categories: etc
layout : single
toc : true 
toc_sticky : true
---



# **제어 반전 컨테이너(IoC)**

- 스프링의 가장 중요하고 핵심적인 기능
- 제어 반전, 제어의 반전, 역제어는 프로그래머가 작성한 프로그램이 재사용 library의 흐름 제어를 받게 되는 소프트웨어 디자인 패턴
- 자바의 반영을 이용해서 객체의 생명주기를 관리하고 의존성 주입을 통해 각 계층이나 서비스들간의 의존성을 맞춰준다. 이러한 기능들은 주로 환경설정을 담당하는 XML 파일에 의해 설정되고 수행된다.

- 전통적인 프로그래밍에서 흐름은 프로그래머가 작성한 프로그램이 외부 라이브러리의 코드를 호출해서 이용한다. 하지만, 제어 반전이 적용된 구조에서는 외부 라이브러리의 코드가 프로그래머가 작성한 코드를 호출한다. 설계 목적상 제어 반전의 목적은 다음과 같다.
  - 작업을 구현하는 방식과 작업 수행 자체를 분리한다.
  - 모듈을 제작할 때, 모듈과 외부 프로그램의 결합에 대해 고민할 필요 없이 모듈의 목적에 집중할 수 있다.
    - 다른 시스템이 어떻게 동작할지에 대해 고민할 필요 없이, 미리 정해진 협약대로만 동작하게 하면 된다.
    - 모듈을 바꾸어도 다른 시스템에 부작용을 일으키지 않는다.
- DI와 IoC를 적절히 사용하면, 느슨하게 결합된 Application을 개발할 수 있다.
  - 느슨하게 결합된 Applicatoin들은 단위테스트(JUnit)을 하기 쉽다.

### 의존성 주입(DI)

- Dependency Injection
- 스프링에서 선언되어 관리되고 있는 인스턴스를 빈(Bean)이라고 부르고, 그 용도에 따라서 Controller Bean, Service Bean, Repository Bean 과 같이 설정하게 된다.
- 스프링에서 이렇게 선언된 Bean을 `의존성 주입(Dependency Injection : DI)`이라는 방법으로 관리하고 있다.
- 의존성 주입 방법
  - xml설정파일
  - 클래스에서 setter메서드나 생성자
  - Annotation
    - @Autowired : spring아, 이 type에 맞는 것을 찾아서 그거랑 이거랑 연결 시켜줘.
    - @Component : spring아, 이것은 너가 관리해야 하는 Bean이야
- 스프링 Controller에 등록된 Bean을 사용하기 위해서는 Conatiner에 등록된 Bean의 참조 값을 받아와서 사용한다.
- 스프링 Container 혹은 IoC Container에 등록된 Bean들은 개발자가 프로그램 실행 도중에 변경할 수 없기 때문에 일관성있는 Instance를 사용할 수 있게 되는 것이다.
  - 예를 들어, user Controller에 user Service를 의존성 주입(DI)이라는 방법을 통해 사용