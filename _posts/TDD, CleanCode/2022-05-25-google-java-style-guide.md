---
layout: post
title: Google java style guide
author: jyKim
categories: TDD, CleanCode
tags:
- JAVA
---

[원본 문서](https://google.github.io/styleguide/javaguide.html)

## 1 도입

이 문서는 구글의 java 프로그래밍 언어 소스코드를 위한 코딩 표준의 `완전한` 정의이다.  
java 소스 파일은 여기에 있는 규칙을 준수해야만 구글 스타일을 따르는 것으로 설명된다. 

다른 프로그래밍 스타일 가이드 처럼, 서식의 미적인 주제 뿐만 아니라 다른 유형의 컨벤션 혹은 코딩 표준에 대한 영역을 다룬다.  
하지만, 이 문서는 우리가 보편적으로 따르는 `엄격하고 빠른 규칙`에 우선적으로 집중하고 있으며 명확하게 시행할 수 없는 조언은 제공하지 않는다(사람이든 툴이든).  

### 1.1 용어 설명

따로 명시되지 않는 한 이 문서에서는:  
1. `class`는 "일반" class, enum class, interface나 어노테이션 타입(@interface)를 의미하는 데 포괄적으로 사용된다.  
2. (class의) `member`는 포괄적으로 내부 class, field, method, 혹은 constructor를 의미하는 데 포괄적으로 사용된다. 즉, initializer와 주석을 제외한 클래스의 모든 최상위 요소들이다.  
3. `comment(주석)`는 항상 구현 주석을 의미한다. "문서 주석"이라는 구문은 사용하지 않고 일반적인 용어인 "javadoc"을 사용한다.  

문서에 가끔 다른 "용어 설명"이 나타난다.  

### 1.2 가이드 설명  
이 문서의 예시 코드는 비표준이다. 즉, 예시는 구글 스타일이지만 코드를 표현하는 유일한 세련된 방법을 설명하지 않을 수 있다. 
예제에서 나타난 선택적 서식은 규칙으로 주장되어서는 안된다.  

## 2 소스 파일 기본  

### 2.1 파일명

소스 파일의 이름은 그것이 포함한 최상위의 class(반드시 하나 존재)의 대소문자를 구분한 이름과 .java 확장자로 구성된다.  

### 2.2 파일 인코딩 : UTF-8

소스파일은 `UTF-8`로 인코딩한다.  

### 2.3 특수 문자

#### 2.3.1 공백 문자

줄바꿈 문자열을 제외하고 ASCII 가로 공백 문자(Ox20)는 소스 파일의 어디에나 나타날 수 있는 유일한 공백 문자이다.  
이것은 다음을 함축한다 :  

1. 문자열과 문자(character literals)의 다른 모든 공백 문자는 escape 된다.  
2. Tab 문자는 들여쓰기로 사용되지 않는다. 

#### 2.3.2 특수 escape 문자열

[특수 escape 문자열](https://docs.oracle.com/javase/tutorial/java/data/characters.html) 
(\b, \t, \n, \f, \r, \", \' , \\)을 가진 모든 문자는 8진수 escape(e.g. \012)나 유니코드 escape(e.g. \u000a) 대신 사용된다.  

#### 2.3.3 Non-ASCII 문자

나머지 Non-ASCII 문자들은 실제 유니코드 문자(e.g. ∞) 혹은 그에 상응하는 유니코드 escape(e.g. \u221e)가 사용된다.  
문자열 리터럴과 주석 밖에서는 유니코드 escape를 사용하는 것은 강력히 권장되지 않지만 선택은 오직 어떤 것이 코드를 쉽게 읽고 이해할 수 있게 만드는지에 달려있다.  

## 3 소스 파일 구조

소스 파일은 아래와 같은 `순서`로 구성된다:   
1. 있는 경우라면, 라이센스 혹은 저작권 정보  
2. package  
3. import  
4. 정확히 하나의 최상위 class  

각각의 구간을 구분하기 위해 <strong>정확히 한 줄의 공백</strong>이 사용된다.  

### 3.1 있는 경우라면, 라이센스 혹은 저작권 정보  

라이센스나 저작권 정보가 파일에 포함된다면 이 위치에 포함 시킨다.  

### 3.2 package

package문은 <strong>줄바꿈 하지 않는다</strong>. 열 제한(섹션 4.4)이 적용되지 않는다.  

### 3.3 Import

#### 3.3.1 와일드카드를 사용하지 않는다.

static이든 아니든 <strong>와일드카드 import는 사용하지 않는다</strong>.  

#### 3.3.2 줄바꿈하지 않음  

import문은 <strong>줄바꿈 하지 않는다</strong>. 열 제한(섹션 4.4)이 적용되지 않는다.  

#### 3.3.3 순서와 공간  
import는 다음 순서를 따른다:  
1. 한 블록의 모든 static import  
1. 한 블록의 모든 non-static import  

만약 static import와 non-static import가 둘 다 있다면, 공백 한 줄이 두 블록을 구분한다. import문 사이에 다른 공백 줄은 허용되지 않는다.  

각 블록 내에서는 import된 이름이 ASCII 순서로 나타난다. (참고 : '.'이 ';' 앞에 오기 때문에 ASCII 정렬 순서인 import문과는 다르다.)...?  

#### 3.3.4 class는 static import 하지 않음

중첩 static class를 불러오기 위해 static import를 사용하지 않는다. 일반 import로 불러온다.  

### 3.4 class 선언

#### 3.4.1 정확히 하나의 최상위 클래스 선언  

각 최상위 class는 자체 소스파일 안에 있다.  

#### 3.4.2 class 요소의 정렬

member와 initializer의 순서 선택은 학습능력에 큰 영향을 줄 수 있다. 하지만, 그에 대한 하나의 올바른 정답은 없다. 서로 다른 클래스는 다른 방식으로 정렬될 수 있다.  

중요한 것은 각 클래스가 관리자가 설명할 수 있는 어떤 논리적인 순서를 사용하는 것이다.  
예를 들어, 새로운 method는 단지 습관적으로 class의 맨 끝에 추가되면 안된다. 이는 논리적인 순서가 아닌 "추가된 날짜 기준" 정렬이기 때문이다.  

##### 3.4.2.1 오버로드: 절대 분리하지 않음

이름을 공유하는 method는 사이에 다른 구성원이 없는 단일 연속 그룹에 나타난다. 
항상 같은 이름을 갖는 생성자 역시 똑같이 적용된다. 이 규칙은 static 혹은 private 등의 수정자가 다른 method 사이에서도 적용된다.

## 4 서식  

용어 설명: `블록 형식의 구조(block-like construct)`는 class, method 혹은 constructor의 본문을 나타낸다. 
섹션 4.8.3.1과 같이 모든 배열 초기화 블록은 선택적으로 블록 형식의 구조처럼 다뤄질 수 있다.

### 4.1 중괄호  

#### 4.1.1 선택적 중괄호 사용

본문이 비어있거나 오직 하나의 구문을 포함하는 경우에도 `if, else, for, do, while`문과 함께 중괄호가 사용된다. 

람다 표현식과 같은 다른 선택적 중괄호는 여전히 선택가능하다.  

#### 4.1.2 비어있지 않은 블록: K & R style  

중괄호는 비어있지 않은 블록과 블록 형식의 구조에 대하여 Kernighan and Ritchie style ("Egyptian brackets")을 따른다.:  

- 아래의 세부 내용을 제외하고는 여는 중괄호 이전에 줄바꿈이 없다.  
- 여는 중괄호 다음에 줄바꿈.  
- 닫는 중괄호 앞에 줄바꿈.  
- 중괄호가 구문을 종료하거나 method, constructor, named class의 본문을 종료하는 경우, 닫는 중괄호 뒤에 줄바꿈을 한다. 
예를 들어 else나 ','가 뒤에 따라오는 경우에는 중괄호 뒤에 줄바꿈하지 않는다.  
  
예외: 세미콜론(;)으로 끝나는 하나의 명령문에 적용되는 경우 명령문 블록이 나타날 수 있고 이 블록의 여는 중괄호 앞에 줄바꿈이 온다. 
이런 블록들은 일반적으로 지역변수의 범위를 제한하기 위해 도입된다(예: switch문 내부).  

예시:

```java
return () -> {
  while (condition()) {
    method();
  }
};

return new MyClass() {
  @Override public void method() {
    if (condition()) {
      try {
        something();
      } catch (ProblemException e) {
        recover();
      }
    } else if (otherCondition()) {
      somethingElse();
    } else {
      lastThing();
    }
    {
      int x = foo();
      frob(x);
    }
  }
};
```

섹션 4.8.1에 enum class와 관련된 예외가 있다.  

#### 4.1.3 빈블록: 간결화 가능  

빈 블록이나 블록 형식 구조는 K & R style을 따를 수 있다. 
다중 블록 구문(if/else 혹은 try/catch/finally는 직접적으로 다중 블록을 포함한다.)의 한 부분이 아니라면, 괄호를 연 즉시 아무 문자는 줄바꿈이 없는 채로 바로 닫을 수 있다({}).  

예시:  

```java
  // This is acceptable
  void doNothing() {}

  // This is equally acceptable
  void doNothingElse() {
  }

  // This is not acceptable: No concise empty blocks in a multi-block statement
  try {
    doSomething();
  } catch (Exception e) {}
```

### 4.2 블록 들여쓰기: +2 spaces

새로운 블록이나 블록 형식 구조가 시작되면 항상 들여쓰기가 2 spaces 만큼 증가한다. 
블록이 끝나면 들여쓰기는 이전 들여쓰기 수준으로 돌아간다. 
들여쓰기 수준은 블록 내 모든 코드와 주석에 적용된다.  

### 4.3 한 줄에 한 명령문

각 명령문뒤에는 줄바꿈이 따라온다.  

### 4.4 열 제한: 100

자바 코드는 100 문자의 열 제한을 가진다. "문자"는 모든 유니코드의 코드 포인트를 의미한다. 
아래 명시된 사항을 제외하고, 이 제한을 초과하는 모든 줄은 섹션 4.5에서 설명하는 대로 줄바꿈하여야한다.  

*) 각 유니코드의 코드 포인트는 표시 너비가 더 크거나 작더라도 하나의 문자로 계산된다. 
예를 들어 전각문자를 사용한다면, 규칙에서 엄격하게 요구하는 것보다 앞서 줄바꿈 하는 것을 선택 할 수 있다.  

예외:  
1. 열 제한을 준수할 수 없는 행(예: javadoc의 긴 URL 또는 긴 JSNI method 참조)  
2. package와 import 명령문(섹션 3.2, 3.3)  
3. shell에 복사 붙여넣기 가능한 주석의 명령줄  
4. 매우 긴 식별자가 드물게 호출될 때 열 제한을 초과 할 수 있다. 
이 경우 주변 코드에 대한 유효한 래핑은 [google-java-format](https://github.com/google/google-java-format) 에 의해 생성된 것과 같다.  
   
