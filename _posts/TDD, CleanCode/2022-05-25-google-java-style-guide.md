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
2. (class의) `member`는 포괄적으로 내부 class, field, method, 혹은 constructor를 의미하는 데 포괄적으로 사용된다. 즉, initializer와 주석을 제외한 class의 모든 최상위 요소들이다.  
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
문자열 literal과 주석 밖에서는 유니코드 escape를 사용하는 것은 강력히 권장되지 않지만 선택은 오직 어떤 것이 코드를 쉽게 읽고 이해할 수 있게 만드는지에 달려있다.  

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

#### 3.4.1 정확히 하나의 최상위 class 선언  

각 최상위 class는 자체 소스파일 안에 있다.  

#### 3.4.2 class 요소의 정렬

member와 initializer의 순서 선택은 학습능력에 큰 영향을 줄 수 있다. 하지만, 그에 대한 하나의 올바른 정답은 없다. 서로 다른 class는 다른 방식으로 정렬될 수 있다.  

중요한 것은 각 class가 관리자가 설명할 수 있는 어떤 논리적인 순서를 사용하는 것이다.  
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
   
### 4.5 줄바꿈
   
용어 설명: 합리적으로 한 줄을 차지할 수 있는 코드를 여러줄로 나누는 것을 줄바꿈이라고 한다.  

모든 상황에서 어떻게 줄바꿈이 이루어져야하는지 보여주는 포괄적이고 결정적인 공식은 없다. 
매우 자주 같은 코드 조각에 대한 여러가지 유효한 줄바꿈 방식이 있다.  

> 참고: 줄바꿈의 일반적인 이유는 열 제한을 넘는 것을 피하는 것이지만, 코드가 열 제한에 적합하더라도 작성자의 재량에 따라 줄바꿈될 수 있다.  

> 팁: method 또는 지역변수를 추출하는 것은 줄바꿈 할 필요 없이 문제를 해결할 수 있다.?  

#### 4.5.1 줄 중단 위치  

줄바꿈의 주요 지침은 더 높은 구문 수준에서 줄을 중단하는 것이다. 또한:  

1. 비 할당 연산자(할당 연산자가 아닌 연산자)에서 줄이 중단되면 해당 기호 앞에서 줄이 중단된다. 
   (이는 C++과 JavaScript 등 다른 언어에 대한 구글 스타일에서 사용되는 것과는 다른 방식이다.)  
    - 이것은 또한 다음의 "유사 연산자" 기호에도 적용된다:  
      - 구분 점 (`.`)  
      - 메소드 참조에 대한 두 콜론 (`::`)  
      - 유형 제한에서의 앰퍼샌드 (`<T extends Foo & Bar>`)  
      - catch 블록에서의 파이프 (`catch (FooException | BarException e`)  
2. 할당 연산자에서 줄이 중단되면 일반적으로 기호 뒤에 줄 바꿈이 오지만 두 방법 다 허용된다.  
    - 이것은 향상된 for문("foreach")의 "유사 할당 연산자" 콜론에도 적용된다.  
3. method나 constructor 이름은 그 뒤에 오는 여는 괄호(`(`)와 연결된다.  
4. 쉼표(`,`)는 앞에 오는 토큰과 연결된다.  
5. 람다의 본문이 중괄호가 없는 단일 표현식으로 구성된 경우 화살표 바로 뒤에 줄바꿈이 올 수 있다는 점을 제외하고 람다의 화살표 인근에서 
   줄바꿈이 오지 않는다. 예:  
   
```java
MyLambda<String, Long, Object> lambda =
    (String label, Long value, Object obj) -> {
        ...
    };

Predicate<String> predicate = str ->
    longExpressionInvolving(str);
```

> 참고: 줄바꿈의 주 목표는 코드를 반드시 가장 적은 수의 줄에 맞추는 것이 아니라 코드를 명확하게 유지하는 것이다.  

#### 4.5.2 연속된 줄의 들여쓰기 최소 +4 공백  

줄바꿈 시 첫번째 줄(각 연속된 줄)은 적어도 원래 줄보다 +4 들여쓰기된다.  

여러 개의 연속된 줄이 있는 경우, 원하는대로 +4이상 들여쓰기 할 수 있다. 
일반적으로 두 연속 줄은 구문상 병렬 요소로 시작하는 경우에만 동일한 들여쓰기 수준을 사용한다.  

수평 정렬에 대한 섹션 4.6.3은 이전 줄과 특정 토큰을 정렬하기 위해 다양한 수의 공백을 사용하는 권장되지 않는 관행을 다룬다.  

### 4.6 공백  

#### 4.6.1 세로 공백  

하나의 빈 줄이 항상 나타난다:  

1. class의 연속 member 혹은 initializer 사이: field, constructor, method, 중첩 class, 정적 initializer, instance initializer  
    - 예외: 두 개의 연속 field 사이(그 사이에 다른 코드가 없는 경우) 빈 줄은 선택사항이다. 
      이러한 빈 줄은 필드의 field의 논리적 그룹을 만드는 데에 필요에 따라 사용된다.  
    - 예외: enum 상수 사이의 빈 줄에 대해서는 섹션 4.8.1에서 다룬다.  
  
2. 이 문서의 다른 섹션(섹션3, 섹션3.3)이 요구하는 바를 따른다.  

하나의 빈 줄은 또한 가독성을 높이기 위해 어디서든 사용될 수 있다. 
예를 들어 코드를 논리적인 하위 섹션으로 구성하기 위해 명령문 사이에 사용할 수 있다. 
첫번째 member나 initializer 앞이나 클래스의 마지막 member 혹은 initializer 뒤에 오는 빈 줄은 권장하거나 권장하지 않는다.?  

연속적인 여러 빈 줄은 허용되지만 필수(또는 권장)는 아니다.  

#### 4.6.2 가로 공백  

언어 또는 다른 스타일 규칙에서 요구하는 곳을 넘어, literal, 주석, javadoc을 제외하고, 단일 ASCII 공백이 또한 다음의 위치에만 나타난다.  

1. if, for, catch 같은 예약어를 해당 줄에 따라오는 여는 괄호(`(`)와 분리  
2. else나 catch 같은 예약어를 해당 줄에서 앞에오는 닫는 중괄호(`}`)와 분리  
3. 여는 중괄호(`{`) 앞에, 두가지 예외:  
    - `@SomeAnnotation({a,b})` (공백이 사용되지 않음)  
    - `String[][] x = {% raw %}{{"foo"}}{% endraw %};` (아래 9 항목에 따라, `{% raw %}{{{% endraw %}` 사이에 공백이 필요하지 않음)  
4. 이항 또는 삼항 연산자 양 옆. 이것은 또한 아래의 "유사 연산자" 기호에도 적용된다:  
    - 결합형 타입 한정 내에서의 앰퍼샌드: `<T extends Foo & Bar>`  
    - 다수의 예외를 다루는 catch 블록의 파이프: `catch (FooException | BarEcveption e)`  
    - 향상된 for문("foreach")안의 콜론(`:`)  
    - 람다 표현식 안의 화살표: `(String str) -> str.length()`  

    아래의 경우에는 공백이 사용되지 않는다.  
    - method 참조의 두 콜론(`::`), `Object::toString`의 형태로 쓰인다.  
    - 점 구분자(`.`), `object.toString()`의 형태로 쓰인다.  
5. `,:;`의 뒤 혹은 형 변환의 닫는 괄호(`)`) 뒤  
6. 내용과 주석을 시작하는 이중 슬래시(`//`) 사이. 다수의 공백 허용.  
7. 주석을 시작하는 이중 슬래시(`//`)와 주석 글귀 사이. 다수의 공백 허용.  
8. type과 변수선언 사이: `List<String> list`  
9. 배열 initializer의 두 중괄호 내부는 선택이다.  
    - `new int[] {5, 6}`, `new int[] { 5, 6 } 모두 허용된다.  
10. type annotation과 `[]` 나 `...` 사이  

이 규칙은 줄의 시작이나 끝에서 추가 공백을 요구하거나 금지하는 것으로 해석되지 않으며 오직 내부 공간에 대한 것이다.  

#### 4.6.3 수평정렬: 필요 없음  

용어 설명: 수평정렬은 특정 토큰이 앞줄의 특정 토큰 바로 아래 위치시키기 위해 코드에 추가적인 공백을 더하는 관행이다.  

이 관행은 허용되지만 Google Style에서 필요하지 않다. 
이미 사용하던 곳에서 조차 수평정렬을 유지할 필요가 없다.  

정렬이 없다가 정렬을 사용한 예시:  

```java
private int x; // 괜찮다
private Color color; // 이것 또한

private int   x;      // 허용되지만 추후 수정
private Color color;  // 정렬되지 않은 상태로 둘 수 있다.
```

> 팁: 정렬은 가독성에 도움이 되지만 추후 유지관리에 문제를 만든다. 
> 단 한줄만 건드릴 필요가 있는 미래의 변화를 고려해라. 
> 이 변화는 이전에 만족스러웠던 서식을 망칠 수 있고 이는 허용된다. 
> 보다 자주 이것은 코더(아마 당신)가 근처 줄의 공백 또한 조정하도록 촉진하며, 어쩌면 연쇄적인 재형식화를 유발할 수 있다. 
> 이 한 줄의 변화는 이제 "폭발 반경"을 갖는다. 
> 이것의 최악의 결과는 무의미한 바쁜 작업이 될 수 있다. 
> 하지만 기껏해야 버전 기록 정보를 손상시키고 검토자의 속도를 늦추며 병합충돌을 악화시킬 뿐이다.  
 
### 4.7 그룹화 괄호: 권장  

선택적 그룹화 괄호는 작성자와 검토자가 그것이 없어도 코드가 오해되거나 그것이 코드의 가독성에 도움을 줄 합리적인 여지가 없다고 동의할때만 생략된다. 
모든 독자가 모든 java 연산자의 우선순의 테이블을 기억하고 있다고 가정하는 것은 합리적이지 않다.

### 4.8 특수 구조

#### 4.8.1 Enum class  

enum 상수 뒤에 오는 각 콤마 뒤 줄바꿈은 선택이다. 
추가적인 빈 줄(보통은 한 줄) 또한 허용된다. 

```java
private enum Answer {
  YES {
    @Override public String toString() {
      return "yes";
    }
  },

  NO,
  MAYBE
}
```

method와 상수에 대한 documentation이 없는 enum class는 선택적으로 배열 initializer(섹션 4.8.3.1)와 같은 형태를 가질 수 있다.  

```java
private enum Suit { CLUBS, HEARTS, SPADES, DIAMONDS }
```

enum class는 class이기 때문에, class 서식에 대한 모든 다른 규칙들이 적용된다.  

#### 4.8.2 변수 선언  

##### 4.8.2.1 한 선언에 한 변수  

모든 변수 선언 (field나 local) 오직 하나의 변수만 선언한다: `int a, b;` 같은 선언은 사용되지 않는다.  

예외: `for` 루프의 헤더에서는 다중 변수 선언이 허용된다.  

##### 4.8.2.2 필요할 때 선언  

지역변수는 습관적으로 그것이 포함하는 블록 또는 유사 블록 구조의 시작부분에 선언되지 않는다. 
대신, 지역변수는 그 범위를 최소화하기 위해 그것이 처음으로 사용되는 곳 가까이 선언된다. 
지역변수 선언은 일반적으로 initializer를 가지거나 선언된 직후 초기화된다.  

#### 4.8.3 배열  

##### 4.8.3.1 배열 initializer: "유사 블록"이 될 수 있음  

모든 배열 initializer는 선택적으로 "유사 블록 구조"와 같은 형식을 가질 수 있다. 
예를 들어 다음의 코드는 유효하다(전체 목록 아님):  

```java
new int[] {           new int[] {
  0, 1, 2, 3            0,
  }                       1,
  2,
  new int[] {             3,
  0, 1,               }
  2, 3
  }                     new int[]
  {0, 1, 2, 3}
```

##### 4.8.3.2 C 스타일의 배열 선언 미사용  

대괄호는 변수가 아닌 타입에 붙는다: `String args[]` 말고 `String[] args`를 사용  

#### 4.8.4 switch 문  

용어 설명: switch 블록의 중괄호 내부에는 하나 이상의 구문 묶음이 있다. 
각 묶음은 하나 이상의 구문(마지막 묶음의 경우 0개 이상의 구문)이 따라오는 하나 이상의 switch 표지(`case Foo:` 또는 `default:`)로 이루어진다.  

##### 4.8.4.1 들여쓰기  

다른 블록과 마찬가지로 switch 블록의 내용은 +2 들여쓰기한다.  

switch 표지 뒤에는 줄바꿈을 하고 블록을 여는 것처럼 들여쓰기 수준이 +2만큼 증가한다. 
따라오는 switch 표지는 블록이 닫힌 것 처럼 이전 들여쓰기 수준으로 돌아간다.  

##### 4.8.4.2 fall-through: 주석 

switch 블록 내부에서 각 구문 묶음은 즉시 종료되거나(`break`, `continue`, `return`, 예외 발생과 함께) 
실행이 다음 명령문 묶음으로 계속될 수 있음을 나타내기 위한 주석으로 표시된다. 
fall-through에 대한 아이디어를 전달하는 모든 주석이 허용된다(일반적으로 `// fall through`). 
이 특별한 주석은 switch 블록의 마지막 구문 묶음에서는 필요하지 않다. 

```java
switch (input) {
  case 1:
  case 2:
    prepareOneOrTwo();
    // fall through
  case 3:
    handleOneTwoOrThree();
    break;
  default:
    handleLargeNumber(input);
}
```

`case 1:` 뒤에는 주석이 필요 없다는 점에 주목해라. 주석은 오직 구문 묶음의 마지막에 온다.  

##### 4.8.4.3 `default` 표지의 존재  

각 switch문은 코드를 포함하지 않을때에도 `default` 구문 묶음을 포함한다.  

예외: enum 타입에 대한 switch문은 해당 유형의 모든 가능한 값에 대한 명시적 경우를 포함하는 경우 default 구문 묶음이 생략될 수 있다. 
누락된 경우가 있으면 IDE 또는 기타 정적 사례 분석도구가 경고를 표시할 수 있다.  

#### 4.8.5 Annotation  

##### 4.8.5.1 타입 사용 annotation  

타입 사용 annotation은 적용되는 유형의 바로 앞에 나타난다. 
`@Target(ElementType.TYPE_USE)`의 메타 annotation이 붙은 annotation은 타입 사용 annotation이다.  

```java
final @Nullable String name;

public @Nullable Person getPersonByName(String name);
```

##### 4.8.5.2 class annotation

class에 적용되는 annotation은 documentation 블록 바로 뒤에 나타나고 
각 annotation은 자체적인 한 줄로 나열된다(즉, 한 줄에 한 annotation). 
이러한 줄 바꿈은 들여쓰기 수준이 증가하지 않는다. 예시:  

```java
@Deprecated
@CheckReturnValue
public final class Frozzler { ... }
```

##### 4.8.5.3 method와 constructor annotation  

method와 constructor의 annotation에 대한 규칙은 이전 섹션(섹션 4.8.5.2)과 같다. 예시:  

```java
@Deprecated
@Override
public String getNameIfPresent() { ... }
```

예외: 매개변수가 없는 하나의 annotation은 signature의 첫번째 줄가 함께 나타날 수 있다. 예시:  

```java
@Override public int hashCode() { ... }
```

##### 4.8.4.5.4 field annotation  

field에 적용되는 annotation 또한 documentation 블록 바로 뒤에 나타난다. 
하지만 이 경우 여러 개의 annotation(매개변수화 가능)은 같은 줄에 나열될 수 있다; 예시:  

```java
@Partial @Mock DataLoader loader;
```

##### 4.8.5.5 매개변수와 지역 변수 annotation  

매개변수나 지역변수의 annotation의 서식에 대해서는 특정한 규칙이 없다(물론 타입 사용 annotation일 때를 제외하고).  

#### 4.8.6 주석  

이 섹션에서는 구현 주석을 다룬다. Javadoc에 대한 것은 Section 7에 분리되어있다.  

모든 줄바꿈 앞에 구현 주석이 뒤따르는 임의의 공백이 올 수 있다. 
이러한 주석은 공백이 아닌 줄로 표현한다.  

##### 4.8.6.1 블록 주석 형식  

블록 주석은 주변 코드와 같은 수준으로 들여쓰기 된다. 
그것은 `/* ... */` 형식이나 `// ...` 형식일 수 있다. 
여러 줄 `/* ... */` 주석의 경우 이어지는 줄은 *로 시작해야 이전 줄의 *에 맞춰 정렬된다.  

```java
/*
 * This is          // And so           /* Or you can
 * okay.            // is this.          * even do this. */
 */
```

주석은 별표나 다른 문자로 표현된 구간에 포함되지 않는다.  

> 팁: 여러 줄의 주석을 작성할 때, 필요에 따라 줄을 다시 감싸기 위해 자동 코드 포맷터를 사용하길 원한다면 `/* ... */` 형식일 사용해라(단락 스타일). 
> 대부분의 포맷터는 `// ...` 형식의 주석 블록에서 줄을 다시 감싸지 않는다.   
 
#### 4.8.7 제어자  

class와 member 제어자가 존재한다면 그것은 Java 언어 명세가 권장하는 순서로 나타난다.  

```text
public protected private abstract default static final transient volatile synchronized native strictfp
```

#### 4.8.8 숫자 literal  

긴 값의 정수 literal은 대문자 L 접미사를 사용하고 소문자는 사용하지 않는다(숫자 1과의 혼동을 피하기 위해). 
예를 들어 `3000000000l`를 사용하지 않고 `3000000000L`를 사용한다.  
