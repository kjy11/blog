---
layout: post
title: IntelliJ에서 JUnit 사용 시 설정
author: jyKim
categories: TDD, CleanCode
tags:
- JUnit
- IntelliJ
---

클래스 내의 단일 메소드 실행 시 다음과 같은 오류가 난다면

```text
0 containers and 1 tests were Method or class mismatch
```

*) Preferences -> Build, Execution, Deployment -> Build Tools -> Gradle 에서

Build and run using과 Run tests using의 속성을 Intellij IDEA로 변경

