---
layout: post
title: Junit
date: 2022-12-21 10:00:00
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

![Macbook]({{site.baseurl}}/assets/img/JUnit모듈.png)



