---
title:  "DailyUp 어플리케이션 개발 - 023"
excerpt: ""

categories:
  - android-log
tags:
  - [Android, 안드로이드, Portfolio, 포트폴리오, Log, 개발일지]

toc: true
toc_sticky: true
 
date: 2026-05-07
last_modified_at: 2026-05-07
---

# 💡 1. 진행한 작업
- 알림에 일정 등록 시 지정한 아이콘이 표현되도록 기능 추가.
- MainActivity 상단 영역이 상단바와 겹쳐지는 문제 수정.
- 앱 알림에 필요한 알림 권한 요청 시 거부 케이스에 대한 케이스 추가.
<br><br><br>
<!-- ---------- -->



# 💡 2. 알게 된 점
- Notification의 Builder Method인 setSmallIcon은 알파 채널만 사용한다고 한다. 그래서 단순하게 Drawable의 Resource ID만 넣어서 사용할 경우 기본적으로 알파가 투명하기 때문에 문제 없이 작동하지만 런타임 중에 확인해보면 투명해서 유저 눈에 보이지 않는다. 그래서 아이콘을 표현하고 싶다면 setLargeIcon 이라는 Builder Method를 사용해야 하며 사용할 아이콘을 Bitmap으로 변환시켜서 넣어야 한다.
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
- 일정 알림에 아이콘 표시 및 일정 상세 보기로 이동하는 기능.
<br><br><br>
<!-- ---------- -->