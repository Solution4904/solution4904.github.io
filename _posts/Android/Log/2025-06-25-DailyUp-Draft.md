---
title:  "DailyUp 어플리케이션 개발 - 004"
excerpt: ""

categories:
  - android-log
tags:
  - [Android, 안드로이드, Portfolio, 포트폴리오, Log, 개발일지]

toc: true
toc_sticky: true
 
date: 2025-06-25
last_modified_at: 2025-06-25
---

# 💡 1. 진행한 작업
- ScheduleList Recyclerview에서 아이템 클릭 후 편집 완료 시 SharedPreference에도 변경된 데이터로 저장.
- Schedule을 추가 및 편집하는 부분에 보일러 플레이트를 함수화 시켜서 활용성을 높임.
<br><br><br>
<!-- ---------- -->



# 💡 2. 알게 된 점
- registerForActivityResult로 결과 값이 돌아왔을 때, 해당 영역에 기능을 Unit 형태의 Callback 변수를 invoke()하는 방식으로 만들면 호출하는 곳 마다 다른 기능을 실행시킬 수 있는 방식도 가능.
- Collection 내 특정 element를 find, filter, any 등의 Collection Function을 사용하여 찾아내는 기능들을 사용.
<br><br><br>
<!-- ---------- -->



# 💡 3. 트러블슈팅 & 해결 방법
- Schedule을 새로 등록하는 건 계속 문제 없었는데, Recyclerview에서 Schedule을 클릭해서 편집하면 편집된 값의 데이터 반영되지 않고 리스트에도 보여지지 않아서 한참을 해멨는데 차근차근 살펴보니 계속 작업하던 부분은 '추가'버튼으로 Schedule을 등록하는 화면으로 넘어갔을 때만 해당되고 있었고, Recyclerview에서 Schedule을 클릭해서 수정하는 화면으로 넘어가는 부분에 대한 기능이 아니었음. -> 단순한 해프닝이긴 하지만 이렇게 단순한 실수가 발생된 원인은 코드가 난잡하고 각 기능별로 함수화 해놨었다면 덜 헷갈릴 수도 있었는데 보일러 플레이트가 여기저기에 존재해서 발생되었을 가능성이 높다고 생각함. 기능들을 함수화하고 너무 많은 코드가 한 함수에 들어가지 않도록 하는 노력이 필요할 것으로 보임.
<br><br><br>
<!-- ---------- -->



# 💡 4. 개선 사항
- 작성한 함수들의 이름이 모호한 이름을 띄는 것들이 보임. 한 함수에 들어가는 코드를 줄이고 직관적인 네이밍이 필요.
<br><br><br>
<!-- ---------- -->



# 💡 5. 다음 목표
- Schedule에 이미지 버튼에 이미지 리소스가 나타나도록 하고 이 데이터가 SharedPreference를 통해 저장/불러오기 되도록 구현.
- Schedule에 이미지 버튼 기능 구현
<br><br><br>
<!-- ---------- -->