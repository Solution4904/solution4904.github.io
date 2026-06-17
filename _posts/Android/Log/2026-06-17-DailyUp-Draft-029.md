---
title:  "DailyUp 어플리케이션 개발 - 029"
excerpt: ""

categories:
  - android-log
tags:
  - [Android, 안드로이드, Portfolio, 포트폴리오, Log, 개발일지]

toc: true
toc_sticky: true
 
date: 2026-06-17
last_modified_at: 2026-06-17
---

# 💡 1. 진행한 작업
- Intent로 data class를 전달하던 방식을 Parcelable 전달로 변경.
- 모든 데이터 작업이 메인 스레드에서 진행되고 있어 IO, Default 스레드로 분할.
- PendingIntent에 필요한 모든 데이터를 호출하는 곳에서 전달, 중복호출 하던 부분을 id 값만 전달받아 조회해서 사용하도록 수정.
<br><br><br>
<!-- ---------- -->



# 💡 2. 알게 된 점
- 기본적으로 모든 호출은 지정해주지 않는 이상 메인 스레드에서 담당하며, 그 밖에 데이터를 처리하는 IO, 연산을 처리하는 Default 등이 있다. 메인 스레드에서 모든 작업을 처리하면 ANR, 렉, 앱 다운 등이 발생한다.
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
- Dispatcher를 설정해주면서 기존의 호출하던 함수들이 suspend fun이 되고, lifeCycleScope, VireModelScope 등을 사용해 호출하는 부분들에 대한 이해 필요.
- 코드 정리, 리팩토링, 개선
<br><br><br>
<!-- ---------- -->