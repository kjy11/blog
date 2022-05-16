---
layout: post
title: 7. List Abstraction
author: jyKim
categories: 자료구조
tags:
- JAVA
- Data Structures & Algorithms in Java
---

#### 참고 서적
Michael T. Goodrich et al., 『Data Structures & Algorithms in Java - 6th Edition, John Wiley & Sons Singapore Pte.Ltd(2015)

# List Abstraction

## 7.1 The List ADT(배열의 추상 자료형)

**) 추상 자료형 : 자료와 자료의 연산에 대한 내용, 구체적인 구현방법을 명시하지는 않는다.

- size() : 배열의 요소 개수 반환  
- isEmpty() : 배열이 비었는지여부를 boolean 값으로 반환  
- get(i) : index가 i인 요소를 반환, i가 0과 size()-1 사이의 값이 아니라면 예외 반환  
- set(i, e) : index가 i인 요소를 e로 치환하고 기존에 있던 요소를 반환, i가 0과 size()-1 사이의 값이 아니라면 예외 반환  
- add(i, e) : index i에 새로운 요소 e를 삽입, 기존의 index i부터의 값들은 index가 한 칸씩 밀림, i가 0과 size()-1 사이의 값이 아니라면 예외 반환  
- remove(i) : index i인 요소를 제거, 이후에 있던 값들은 앞으로 한칸씩 당겨짐, i가 0과 size()-1 사이의 값이 아니라면 예외 반환  

## 7.2 Array 기반 List

array A(단순 배열, 고정 길이)에 대하여,  
- get(i), set(i, e)는 A[i]로 쉽게 접근할 수 있다. -> O(1)  
- add(i, e), remove(i)의 경우 이후의 값들을 앞으로 당기거나 뒤로 미는 작업이 필요하다 -> O(n)  

### 동적 array

처음에 배열 A는 특정 용량 N으로 지정되어있다. 배열이 가득 찬 상태에서 add가 발생하면 다음 단계를 실행한다.  
- 더 큰 용량(보통 2N)의 배열 B를 할당한다.  
- k=0에서 k=N-1까지 B[k] = A[k]를 실행한다.  
- A = B로 세팅한다.  
- A에 새로운 요소를 추가한다.  

**) 배열이 2n으로 늘어날 때는 일련의 push 메소드가 O(n)의 시간복잡도를 가지지만 상수(k)만큼 씩 고정으로 늘어날때는 Ω(n²)의 시간복잡도를 가지게 된다.
