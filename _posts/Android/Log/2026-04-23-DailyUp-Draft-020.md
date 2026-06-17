---
title:  "DailyUp 어플리케이션 개발 - 020"
excerpt: ""

categories:
  - android-log
tags:
  - [Android, 안드로이드, Portfolio, 포트폴리오, Log, 개발일지]

toc: true
toc_sticky: true
 
date: 2026-04-23
last_modified_at: 2026-04-23
---

# 💡 1. 진행한 작업
- NumberPicker의 텍스트 부분의 EditText 기능 제거.
- 일정 등록 시 시간 값이 현재 시간으로 초기화.
- 일정 편집 시 시간 값이 저장되어 있는 시간으로 초기화.
<br><br><br>
<!-- ---------- -->



# 💡 2. 알게 된 점
- 일정의 시간을 지정해주기 위해 NumberPicker를 사용했다.
- ScrollView에선 모든 View들의 세로 크기가 동일하거나 동일한 비율로 지정될 수 없다.
<br><br><br>
<!-- ---------- -->



# 💡 3. 트러블슈팅 & 해결 방법
- 일정 등록 화면에서 입력을 받는 레이아웃들은 모두 ScrollView > LinearLayout > TextView, EditText였고 LinearLayout의 세로 크기를 wrap content로 설정해두었었다. 1차 프로토타입 작성 당시 세로로 나열된 입력 폼들이 모두 동일한 세로 크기를 갖고 있었는데, 이번에 NumberPicker를 추가했더니 이 부분만 투명한 공간까지 모두 공간이 지정되었다. 처음에는 다른 Layout들에서처럼 0dp나 weight, percent로 시도했었는데 아무런 차이가 없었다. AI에게 물어보니 ScrollView의 특성상 세로 길이는 내부의 자식들에 따라 유동적이고 자식들은 부모 ScrollView의 세로 길이는 무한하다고 전달받기 때문에 자식들의 세로 길이는 비율과 같은 값으로는 지정할 수 없다고 한다. 여러가지 방법을 생각해봤으나 결국 TextView나 EditText는 기본적으로 48dp~의 크기를 갖고 있기 때문에 따로 지정하지 않는다면 48dp로 지정해주면 문제가 없을 것이라는 AI 의견에 따라 일단 48dp로 지정해두었다. 만약 해상도가 다른 기기들에서 테스트 해봤을 때 문제가 생긴다면 다른 방법을 생각해봐야겠다.
<br><br><br>
<!-- ---------- -->



# 💡 4. 개선이 필요한 사항
- 
<br><br><br>
<!-- ---------- -->



# 💡 5. 다음 목표
- 일정 등록, 편집 시에 반복 주기 라디오버튼이 무조건 첫번째로 선택되어 나오는 문제 수정 필요.
<br><br><br>
<!-- ---------- -->