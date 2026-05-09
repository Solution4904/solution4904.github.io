---
title:  "DailyUp 어플리케이션 개발 - 024"
excerpt: ""

categories:
  - android-log
tags:
  - [Android, 안드로이드, Portfolio, 포트폴리오, Log, 개발일지]

toc: true
toc_sticky: true
 
date: 2026-05-09
last_modified_at: 2025-05-09
---

# 💡 1. 진행한 작업
- 일정 알림 푸시를 누르면 일정의 상세 페이지가 실행되도록 기능 구현.
- 주간 달력에 날짜 이동 시 간혹 날짜 데이터가 비정상적으로 표현되던 문제 수정.
- 주간 달력의 날짜 아이템이 빈 공간 없도록 나열되도록 수정.
<br><br><br>
<!-- ---------- -->



# 💡 2. 알게 된 점
- lifeCycleScope.withStarted 라는 라이프사이클 인지 코루틴 이라는 기능이 있다.
- RecyclerView의 아이템들의 크기는 match parent 로 설정해두어야 parent인 RecyclerView에 추가되었을 때 정상적으로 표시된다.
<br><br><br>
<!-- ---------- -->



# 💡 3. 트러블슈팅 & 해결 방법
- 일정 알림 푸시를 누르면 일정의 상세 페이지가 나오도록 구현하고 싶었는데, 기능을 넣어도 메인 화면으로 실행되는 문제가 있었다. 단순히 기능 구현 실수라기엔 따로 에러도 뜨지 않아서 알아보니 Navigation의 collector가 아직 활성화되지 않은 상태로 일정 상세 페이지로 이동하는 이벤트를 emit해서 이동되지 않았던 것 같다. 그래서 collector가 활성화 되고 난 이후에 Navigation 되도록 해당 시점을 Lifecycle의 Start 이후에 실행되도록 호출 시점을 변경했다. lifeCycleScope.withStarted나 onStart()나 호출 시점이 같으니 onStart()에 넣으려 했는데 onCreate() 시점에 최초 1회만 실행되는 지금과 달리 onStart()에 두게 되면 의도와 다르게 여러 번 실행되는 문제를 막기 위해 lifeCycleScope로 조정했다.
<br><br><br>
<!-- ---------- -->



# 💡 4. 개선이 필요한 사항
- 
<br><br><br>
<!-- ---------- -->



# 💡 5. 다음 목표
- 일정 통계 화면 및 기능 구현.
<br><br><br>
<!-- ---------- -->