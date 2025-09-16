---
title:  "DailyUp 어플리케이션 개발 - 013"
excerpt: ""

categories:
  - android-log
tags:
  - [Android, 안드로이드, Portfolio, 포트폴리오, Log, 개발일지]

toc: true
toc_sticky: true
 
date: 2025-09-15
last_modified_at: 2025-09-15
---

# 💡 1. 진행한 작업
- MVVM 아키텍처 적용.
- Observer, Event Flow 패턴 적용.
- Calendar Adapter에서 계산하던 날짜 기능들을 CalendarUtil Class에 요청하고 받아오는 방식으로 개선.
- MainView Class에 작성되어 있던 기능들을 MainViewModel로 이전.
- MainView xml Data Binding.
<br><br><br>
<!-- ---------- -->



# 💡 2. 알게 된 점
- Event Flow 패턴에서 Event를 선언해두는 sealed class에서 각 Event들이 object 혹은 data class로 선언되어 있는 차이가 무엇인지 몰랐는데 object 타입은 파라미터가 없을 때, data class 타입은 파라미터가 있을 때 사용한다고 한다.
- Event Flow를 사용한 MVVM 아키텍처를 적용하는 방법을 알게 됐다.
- 
<br><br><br>
<!-- ---------- -->



# 💡 3. 트러블슈팅 & 해결 방법
- MainView는 MainViewModel과 ScheduleViewModel 두 개를 모두 갖고 있다. 예를 들어 MainView에서 이미 존재하는 일정을 수정하려고 하면 수정하는 기능은 MainViewModel에서 구현, 실행되어야 하지만 일정의 수정은 ScheduleViewModel의 기능이다. 처음 들었던 구현 방법은 MainView에서 일정을 수정하는 MainViewModel의 기능을 수행하고 MainViewModel에서 ScheduleViewModel에 접근해 해당 일정을 수정시키는 것을 생각해봤는데, 구조상 너무 이상했다. ViewModel이란 자신과 연관있는 View나 Model과는 연관되더라도 다른 ViewModel 즉 ViewModel간에 접근하는 게 맞는 방법인지 의문을 가졌고 조사해보니 아키텍처상 틀린 방법이라는 것을 알았다. 그래서 Event Flow를 통해 View에서 Event를 감지하고 각 Event 별로 실행되어야 하는 기능을 가진 ViewModel에 접근, 실행하도록 구성했다. 프로젝트 규모 때문인지 본래 코드보다 굉장히 복잡해졌지만 규모나 기능이 더 생길 경우를 생각해봤을 때 더 편리할 것 같다.
<br><br><br>
<!-- ---------- -->



# 💡 4. 개선이 필요한 사항
- 
<br><br><br>
<!-- ---------- -->



# 💡 5. 다음 목표
- MVVM 아키텍처를 위한 Observer, Event Flow 이어서 적용.
<br><br><br>
<!-- ---------- -->