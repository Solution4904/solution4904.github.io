---
title:  "DailyUp 어플리케이션 개발 - 033"
excerpt: ""

categories:
  - android-log
tags:
  - [Android, 안드로이드, Portfolio, 포트폴리오, Log, 개발일지]

toc: true
toc_sticky: true
 
date: 2026-08-19
last_modified_at: 2026-08-19
---

# 💡 1. 진행한 작업
- 
<br><br><br>
<!-- ---------- -->



# 💡 2. 알게 된 점
- @RequiresApi 어노테이션은 런타임 가드가 아니여서, 컴파일 경고만 없애줄 뿐 실제 실행을 막진 않는다.
<br><br><br>
<!-- ---------- -->



# 💡 3. 트러블슈팅 & 해결 방법
- 실제 Galaxy 10 Note 기기에서 일정 추가 버튼 터치 시 FATAL EXCAPTION:NoSuchMethodError 강제 종료. 
-> Intent.getParcelableExtra()는 API 33에서 추가된 프레임워크 메서드인데 Galaxy 10 Note 기기의 API는 Android 12(API 31)이여서 지원되지 않음.
-> 문제가 되는 Intent.getParcelableExtra()를 IntentCompat.getParcelableExtra()로 수정
- 실제 Galaxy 10 Note 기기에서 일정 추가 화면에서 데이터를 넣고 저장 시 FATAL EXCAPTION:DateTimeParceExcaption 강제 종료.
-> 데이터를 전달하는 AddScheduleActivity.kt에선 SCHEDULE_MODEL 키 값으로 보내고 있지만, 데이터를 받는 MainActivity.kt에서 SCHEDULE_TYPE, SCHEDULE_ID 등 개별 키로 사용하려하고 있음.
-> 키 값에 해당하는 데이터가 없으니 getStringExtra()는 null을 반환하지만 .toString이 이를 "null"로 변환시켜버림.
-> "null"로 변환된 데이터가 LocalDate.parse("null")로 사용되어서 결국 DateTimeParceException 발생.
<br><br><br>
<!-- ---------- -->



# 💡 4. 개선이 필요한 사항
- 
<br><br><br>
<!-- ---------- -->



# 💡 5. 다음 목표
- QA
- 일정 등록 화면 진입 시 날짜와 시간이 현재와 무관하게 초기화 되고 있음.
- 일정 등록 화면 진입 시 아이콘이 비어 있음.
- 등록된 일정의 푸시 알림을 누르면 앱이 실행되고 "해당 일정이 존재하지 않습니다"고 뜸.
- 앱 실행 시 오늘에 해당하는 일정이 로드되지 않은 상태로 초기화 됨.
<br><br><br>
<!-- ---------- -->