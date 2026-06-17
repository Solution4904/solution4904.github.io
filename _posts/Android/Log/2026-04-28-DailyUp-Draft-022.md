---
title:  "DailyUp 어플리케이션 개발 - 022"
excerpt: ""

categories:
  - android-log
tags:
  - [Android, 안드로이드, Portfolio, 포트폴리오, Log, 개발일지]

toc: true
toc_sticky: true
 
date: 2026-04-28
last_modified_at: 2026-04-28
---

# 💡 1. 진행한 작업
- Require 어노테이션 제거 (desugaring)
- 일정의 알림 기능 추가 (Notification, BroadcastReceiver, )
<br><br><br>
<!-- ---------- -->



# 💡 2. 알게 된 점
- Require API~ 어노테이션이 해당하는 API 이후부터 사용가능한 일종의 조건문으로 이해하고 있었는데 desugaring 이라는 걸로 어느 정도 해소시킬 수 있다.
- 앨비스 연산자에서 else 값이 return 이면 변수 값에 return을 할당하는 게 아니고 early return이 된다.
<br><br><br>
<!-- ---------- -->



# 💡 3. 트러블슈팅 & 해결 방법
- 
<br><br><br>
<!-- ---------- -->



# 💡 4. 개선이 필요한 사항
- 모든 Activity가 상단 상태바를 무시하고 전체 화면에서 표현되고 있음.
<br><br><br>
<!-- ---------- -->



# 💡 5. 다음 목표
- 일정 알림에 아이콘 표시 및 일정 상세 보기로 이동하는 기능.
- 알림 권한 요청 시 거부 케이스 구현.
<br><br><br>
<!-- ---------- -->