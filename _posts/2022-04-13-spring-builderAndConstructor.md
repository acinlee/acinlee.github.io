---
layout: post
title: Builder 어노테이션 사용시 @NoArgsConstructor 와 @AllArgsConstructor 함께 사용하는 이유
---
### 생성자 생성 기본 개념
@Builder, @NoArgsConstructor, @AllArgsConstructor 들을 논하기 전에 객체 생성에 대해 먼저 알아 본다.   
### 객체 생성 방식
- 생성자 패턴
- 빌터 패턴

생성자 패턴은 Constructor
``` java
  public Class CarImpl {
    private String id = "1";
    private STring name = "carTest";
    
    Car car1 = new Car(id, name);
    Car car2 = new Car(name, id);
```
Car 객체를 구현한 위의 코드를 보면 일반 생성자 패턴 사용시 파라미터에 대한 정확성 및 오류를 검출하기 힘들다.   
즉, 파라미터가 정확하게 전달 되었는지 확인하기 힘들다. 해당 문제를 해결하기 위해 @Builder 패턴을 사용한다.

### @Builder
@Builder 어노테이션은 클래스 레벨에 붙이거나 생성자에 붙여주면 파라미터를 활용하여 빌더 패턴을 자동으로 생성해준다.   
   
클래스 레벨의 @Builder   
    
생성자 레벨의 @Builder

### @NoArgsConstructor
+ 파라미터가 없는 기본 생성자 생성

***
