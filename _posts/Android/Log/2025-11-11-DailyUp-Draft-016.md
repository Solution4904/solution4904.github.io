---
title:  "DailyUp 어플리케이션 개발 - 016"
excerpt: ""

categories:
  - android-log
tags:
  - [Android, 안드로이드, Portfolio, 포트폴리오, Log, 개발일지]

toc: true
toc_sticky: true
 
date: 2025-11-11
last_modified_at: 2025-11-11
---

# 💡 1. 진행한 작업
- MVVM 아키텍처를 위한 Observer, Event Flow 이어서 적용.
<br><br><br>
<!-- ---------- -->



# 💡 2. 알게 된 점
- Kotlin 표준 라이브러리의 .takeIf 라는 걸 알게되어서 사용했다.
- ViewModel을 사용하기 위해 선언할 때 by viewModels()로 생성했는데, 이 때 다른 곳에서 동일한 ViewModel을 by viewModels()로 생성할 경우 기존의 생성되어 있던 곳에선 ViewModel이 파괴되고 마지막으로 선언한 곳에서 ViewModel이 새롭게 생성된다는 것을 알았다.
<br><br><br>
<!-- ---------- -->



# 💡 3. 트러블슈팅 & 해결 방법
- Schedule을 새로 추가하면 기존에 있던 다른 Schedule 데이터들에 추가되는게 아닌 항상 마지막으로 생성한 Schedule만 저장되고 있는 문제가 있었다. by viewModels()로 인한 문제라는 것을 깨닫고 Schedule을 새로 생성할 시 AddScheduleActivity에서 ScheduleModel을 생성하고 MainActivity로 전달해주도록 수정하고 빌드 테스트를 해봤는데 Schedule의 ID 값이 데이터타입으로 입력되고있는 문제가 있었다. 코드를 타고 올라가며 확인해보니 MutableLiveData<String>("")으로 선언해두어서 생긴 문제였다. 변수 선언 시 초기 값을 랜덤 UUID로 넣어 수정했다.
- 
<br><br><br>
<!-- ---------- -->



# 💡 4. 개선이 필요한 사항
- 상단 주간 달력에서 다른 날짜를 선택하고 Schedule을 추가할 경우 주간 달력에서 선택되어 있던 날짜가 AddScheduleActivity의 날짜 값으로 초기화 되도록 수정 필요.
<br><br><br>
<!-- ---------- -->



# 💡 5. 다음 목표
- MVVM 아키텍처를 위한 Observer, Event Flow 이어서 적용.
- 주간 달력에서 다른 날짜를 클릭하고 Schedule을 생성하면 기존에 저장되어 있던 Schedule 데이터들이 전부 사라지고 새로 추가한 Schedule 한 개의 데이터만 남는 문제 수정.
<br><br><br>
<!-- ---------- -->