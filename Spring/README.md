# Spring

## Spring이란?
* 엔터프라이즈 급 애플리케이션을 만들기 위한 모든 기능을 종합적으로 제공하는 경량화 된 솔루션이다.
* JEE(Java Enterprise Edition)가 제공하는 다수의 기능을 지원하고 있기 때문에, JEE를 대체하는 프레임워크로 자리잡고 있다.
* SpringFramework는 JEE가 제공하는 다양한 기능을 제공하는 것 뿐만 아니라, DI(Dependency Injection)나 AOP(Aspect Oriented Programming)와 같은 기능도 지원한다.
* 자바로 Enterprise Application을 만들 때 포괄적으로 사용하는 Programming 및 Configuration Model을 제공해 주는 Framework로 Application 수준의 인프라 스트럭쳐를 제공한다.
* 개발자가 복잡하고 실수하기 쉬운 Low Level에 신경 쓰지 않고 Business Logic개발에 전념할 수 있도록 해준다.


# Spring의 구조(POJO, PSA, IoC/DI, AOP)

## POJO(Plain Old Java Object)
* 특정 환경이나 기술에 종속적이지 않은 객체지향 원리에 충실한 자바객체
* 테스트하기 용이하며, 객체지향 설계를 자유롭게 적용할 수 있다.

## PSA(Portable Service Abstraction)
* 환경과 세부기술의 변경과 관계없이 일관된 방식으로 기술에 접근할 수 있게 해주는 설계 원칙
* 트랜잭션 추상화, OXM 추상화, 데이터 액세스의 Exception 변환기능 등 기술적인 복잡함은 추상화를 통해 Low Level의 기술 구현 부분과 기술을 사용하는 인터페이스로 분리
* 예를 들어 데이터베이스에 관계없이 동일하게 적용 할 수 있는 트랜잭션 처리방식

## IoC/DI(Inversion of Control/Dependency Injection)
* 스프링에서 객체에 대한 생성과 생명주기를 관리할 수 있는 기능을 제공하는데 이를 IoC Container 또는 Spring Container라고 한다.
* DI는 유연하게 확장 가능한 객체를 만들어 두고 객체 간의 의존관계는 외부에서 다이나믹하게 설정.

## AOP(Aspect Oriented Programming)
* 관심사의 분리를 통해서 소프트웨어의 모듈성을 향상.
* 공통 모듈을 여러 코드에 쉽게 적용가능.
