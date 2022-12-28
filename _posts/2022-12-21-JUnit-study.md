---
layout: post
title: Junit
date: 2022-12-21 00:00:00 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: js-1.png
tags: [JUnit]
---
# JUnit

### 목표 : JUnit을 적용한 spring boot 구축

### 목차
1. 테스트 코드 작성 목적
2. TDD 정의
3. JUnit이란?
4. JUnit 모듈
5. JUnit Life Cycle
6. JUnit Annotation

### 테스트 코드를 작성하는 목적?
- 코드의 안정성 증진
- 기능 추가 및 변경시 발생하는 side-effect를 줄일 수 있음
- 불필요한 코드들이 들어가는 것을 줄이며 해당 코드가 작성된 목적을 명확하게 표현할 수 있음

### TDD 정의
- Test-Driven-Development(테스트 주도 개발) 의 약자
- 테스트를 먼저 설계 및 구축 후 테스트를 통과할 수 있는 코드를 작성하는 방식
- 애자일 개발 방식 중 하나
  - 코드 설계시 최초 목표에 맞춘 테스트를 구축하여 그에 맞게 설계 하기 때문에 불필요한 코드들을 줄일 수 있다

### JUnit 이란?
- Java 진영의 Test Framework
- 단위 테스트 (Unit Test)를 위한 도구를 제공
  - 단위 테스트
    - 코드의 특정 모듈이 의도된 대로 동작하는지 테스트 하는 절차를 의미
    - 모든 함수와 메스드에 대한 각각의 테스트 케이스를 작성 하는 것
- 어노테이션 기반으로 테스트를 지원
- Assert를 통해 테스트 케이스의 기대값에 대해 수행 결과를 확인할 수 있음
- JUnit은 크게 Jupiter, Platform, Vintage 모듈로 구성

### JUnit 모듈
1. JUnit Jupiter
   - TestEngine Api 구현체로 JUnit5 를 구현함
   - 개발자가 테스트 코드를 작성할 때 사용
2. JUnit Platform
   - TestEngine 인터페이스 (Test를 발견하고 Test 계획을 생성, 수행 및 결과 보고)
   - Test를 실행하기 위한 뼈대
   - Platform = TestEngine Api + Console Launcher + JUnit Based Runner ...)
3. JUnit Vintage
   - TestEngine Api 구현체로 JUnit3,4 를 구현함
   - 기존 JUnit 3,4 버전으로 작성된 테스트 코드 실행할 때 사용됨
4. 모듈 이미지

![JUnitModule]({{site.baseurl}}/assets/img/JUnit모듈.png)

### JUnit Life Cycle

| Annotation | Description                              |
|:----------:|:-----------------------------------------|
|   @Test    | 테스트용 메소드를 표현하는 어노테이션                     |
| @BeforEach | 각 테스트 메소드가 시작되기 전에 실행되어야 하는 메소드를 표현      |
| @AfterEach | 각 테스트 메소드가 시작된 후 실행되어야 하는 메소드를 표현        |
| @BeforeAll | 테스트 시작 전에 실행되어야 하는 메소드를 표현(static 처리 필요) |
| @AfterAll  | 테스트 종료 후에 실행되어야 하는 메소드를 표현(static 처리 필요) |
  
### JUnit Annotation
1. @SpringBootTest
   - 통합 테스트 용도로 사용
   - @SpringBootApplication을 찾아 하위의 모든 Bean을 스캔하여 로드함
   - 모든 Bean을 스캔하여 로드 한 후 Test용 Application Context를 만들어 Bean을 추가하고, MockBean을 찾아 교체
2. @ExtendWith
   - JUnit4에서 @RunWith로 사용되던 어노테이션이 @ExtendWith로 변경됨
   - 메인으로 실행될 Class 지정 가능
   - @SpringBootTest에는 기본적으로 @ExtendWith가 추가되어 있음
3. @WebMvcTest(Class명.class)
   - ()에 작성된 클래스만 실제로 로드하여 테스트를 진행
   - 매개변수를 지정해주지 않으면 @Controller, @RestController 등 컨트롤러와 연관된 Bean이 모두 로드 됨
   - 스프링의 모든 Bean을 로드하는 @SpringBootTest 대신 컨트롤러 관련 코드만 테스트할 경우 사용
4. @Autowired about Mockbean
   - Controller의 Api를 테스트하는 용도인 MockMvc 객체를 주입 받음
   - perform() 메소드를 활용해 컨트롤러의 동작 확인 가능
   - andExpect(), andDo(), andReturn()등의 메소드를 같이 활용
5. MockBean
   - 테스트할 클래스에서 주입 받고 있는 객체에 대해 가짜 객체를 생성
   - 해당 객체는 실제 행위를 하지 않음
   - given() 메소드를 활용하여 가짜 객체의 동작에 대해 정의하여 사용 가능
6. @AutoConfigureMockMvc
   - spring.test.mockmvc의 설정을 로드하면서 MockMvc의 의존성을 자동으로 주입
   - MockMvc 클래스는 REST api 테스트를 할 수 있는 클래스
7. @Import
   - 필요한 Class들을 Configuration으로 만들어 사용할 수 있음
   - Configuration 컴포넌트 클래스도 의존성 설정 가능
   - Import 된 클래스는 주입으로 사용 가능

### 통합 테스트
통합 테스는 여러 기능을 조합하여 전제 비즈니스 로직이 제대로 동작하는지 확인하는 것을 의미

통합 테스트의 경우 @SpringBootTest를 사용하여 진행
- @SpringBootTest는 @SpringBootApplication을 찾아가서 모든 Bean을 로드
- 따라서 테스트를 실행할 때마다 모든 Bean을 스캔하고 로드하는 작업이 반복되어 매번 무거운 작업이 수행됨 

### 단위 테스트
단위 테스트는 프로젝트에 필요한 모든 기능에 대한 테스트를 각각 진행하는 것을 의미

#### F.I.R.S.T 원칙
- Fast : 테스트 코드의 실행은 빠르게 진행되어야 함
- Independent : 독립적인 테스트가 가능해야 함
- Repeatable : 테스트는 매번 같은 결과를 만들어야 함
- Self-Validating : 테스트는 그 자체로 실행하여 결과를 확인할 수 있어야 함
- Timely : 단위 테스트는 비즈니스 코드가 완성되기 전에 구성하고 테스트가 가능해야 함

`코드가 완성되기 전부터 테스트가 따라와야 한다는 TDD의 원칙을 담고 있음`
