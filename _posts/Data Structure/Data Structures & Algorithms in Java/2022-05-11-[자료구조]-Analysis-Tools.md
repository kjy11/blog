---
layout: post
title: 4.Analysis Tools
author: jyKim
categories: 자료구조
tags:
- JAVA
- Data Structures & Algorithms in Java
---

#### 참고 서적
Michael T. Goodrich et al., 『Data Structures & Algorithms in Java - 6th Edition, John Wiley & Sons Singapore Pte.Ltd(2015)

# Analysis Tools

좋은 자료구조와 알고리즘을 판단하기 위한 척도로 `실행시간(running times)`을 사용  

## 4-1. Empirical Analysis(실증분석)

간단한 방법은 실제 실행시켜서 경과된 시간을 확인하는 것  

System.currentTimeMillis()는 `January 1, 1970 UTC`로부터 현재까지 지난 시간을 milliseconds로 나타내는 함수이다.

```java
long startTime = System.currentTimeMillis();
/* 알고리즘 실행 */
long endTime = System.currentTimeMillis();
long elapsed = endTime - startTime; // 경과 시간 
```

**) 매우 빠른 수행의 경우 `System.nanoTime()`을 사용할 수 있다.  

다양한 크기의 입력 대하여 독립적인 실험이 수행되어야 한다.  
x축을 입력의 크기(n), y축을 실행시간(t)로 두어 입력 크기와 실행시간의 관계를 시각화할 수 있다.  

하지만 위의 방법을 통한 측정은 실행 컴퓨터에 따라 다를 수 있고 심지어는 같은 컴퓨터여도 각각의 실행마다 다를 수 있다.  
이는 CPU(central processing unit)와 메모리를 여러 프로세스가 공유하기 때문이다.  
즉, 실행 시간은 테스트가 수행 될 때 컴퓨터에서 실행되고 있는 다른 프로세스에 의해 영향을 받는다.  

따라서 해당 실험에서 각각의 정확한 실행시간을 신뢰할 수는 없지만 비슷한 환경에서 실행된다면 서로 다른 알고리즘의 비교에는 유의미하다.  

**) String과 StringBuilder의 반복적으로 문자열 덧붙이는 작업의 실행시간을 비교하면 StringBuilder가 훨씬 빠름을 알 수 있다.  

### 문제

1. 같은 하드웨어, 소프트웨어를 사용하지 않으면 직접적으로 두 개의 알고리즘을 비교할 수 없다.  
2. 제한된 테스트 입력의 사용  
3. 실행시간을 확인하기위해 알고리즘을 완전히 구현해야한다.  

### 목표

1. 하드웨어, 소프트웨어에 상관 없이 알고리즘을 비교 하도록  
2. 실제 구현 없이 고수준의 기술(high-level description)로 평가하도록  
3. 모든 가능한 입력을 고려하도록  

### -> 기본 연산 집계

#### 기본 연산 정의

- 변수에 값 할당  
- 객체 참조  
- 수학적 연산(ex. 두 수의 덧셈) 수행  
- 두 수의 비교  
- 인덱스로 배열의 단일 객체에 접근  
- 메소드 호출  
- 메소드 결과값 반환  

각 기본 연산의 실행 시간은 거의 비슷하다고 가정하면 알고리즘의 실행 시간은 수행하는 기본 연산의 총 개수에 비례한다고 볼 수 있다.  

같은 크기의 입력이더라도 입력에 따라 실행시간이 다르다.  
평균 실행시간을 구하려면 가능한 모든 입력과 입력의 분포까지 고려해야하므로 `최악의 경우(Worst-Case)를 기준`으로 분석한다.  

## 4-2. 일반 수학 함수

|constant|logarithm|linear|n-log-n|quadratic|cubic|exponential|
|---|---|---|---|---|---|---|
|1|log n|n|n log n|n<sup>2</sup>|n<sup>3</sup>|a<sup>n</sup>|

오른쪽으로 갈수록 n이 늘어남에 따른 결과값 증가가 급격해진다.  

## 4-3. Big-Oh 표기법

정의 : 모든 정수 n >= n<sub>0</sub>에 대하여 f(n) <= cg(n)을 만족하는 실수 상수 c > 0와 정수 상수 n<sub>0</sub> >= 1가 존재한다면 f(n)은 O(g(n))이라고 한다.  

(참고) n이 무한에 가까워질 때 더 커지는 항(높은 차수의 항)에 주목하여 g(n)을 찾을 수 있다.  

**) 위 4-1에서 언급한 예시에서 String을 사용한 알고리즘은 O(n<sup>2</sup>)이며 StringBuilder를 사용한 알고리즘은 O(n)이다.  
