---
title:  "DailyUp 어플리케이션 개발 - 031"
excerpt: ""

categories:
  - android-log
tags:
  - [Android, 안드로이드, Portfolio, 포트폴리오, Log, 개발일지]

toc: true
toc_sticky: true
 
date: 2026-06-26
last_modified_at: 2026-06-26
---

# 💡 1. 진행한 작업
- 
<br><br><br>
<!-- ---------- -->



# 💡 2. 알게 된 점
- maxOf(a,b, ~) 라는 코틀린 표준 라이브러리 함수를 알았다. 파라미터 값 중 가장 큰 값을 반환한다. 여러 개와 다양한 타입을 지원한다.
- A의 확장함수 B는 A의 함수, 변수에 접근/사용이 가능하다.(단, 해당 함수나 변수가 public이나 internal 타입일 때만 가능.) 여기서 A를 리시버 타입 이라고 한다.
- lengthOfMonth는 java.time 패키지 함수로 해당 월이 총 며칠인지 반환한다.
- YearMonth는 연과 달만 반환하는 java.time 패키지 함수이다. 며칠인지 중요하지 않을 때 사용한다.
- getSharedPreferences(name, mode)에서 mode라는 파라미터 값이 무엇이 있고 어떻게 쓰이는지 궁금했다. 모드는 총 3개가 있고, MODE_PRIVATE 외에 2개는 다른 앱이 읽거나 쓰는 것을 가능하게 하는 모드였는데, 쓰이지도 않고 deprecated 됐다고 한다.
- goAsync는 BroadcastReceiver의 onReceive에서 10초 이내의 짧은 비동기 작업을 안전하게 끝낼 수 있도록 지연시키는 메소드이다. 더 긴 작업은 WorkManager를 사용해야하고 반드시 finish()를 사용해서 끝났음을 명시해야한다.(ANR/리소스 누수)
<br><br><br>
<!-- ---------- -->



# 💡 3. 트러블슈팅 & 해결 방법
- 
<br><br><br>
<!-- ---------- -->



# 💡 4. 개선이 필요한 사항
- 
<br><br><br>
<!-- ---------- -->



# 💡 5. 다음 목표
- 코드 정리, 리팩토링, 개선
<br><br><br>
<!-- ---------- -->