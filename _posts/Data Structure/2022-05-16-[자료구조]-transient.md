---
layout: post
title: transient
author: jyKim
categories: 자료구조
tags:
- JAVA
---

```java
private transient int i;
```

변수 선언 시 사용  
일시적인 변수로 객체의 영구적인 상태에 저장되지 않음  
직렬화 시 변수 무시됨

#### 참고
https://docs.oracle.com/javase/specs/jls/se8/html/jls-8.html#jls-8.3.1.3
