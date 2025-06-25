---
title:  "DailyUp 어플리케이션 개발 - 003"
excerpt: ""

categories:
  - android-log
tags:
  - [Android, 안드로이드, Portfolio, 포트폴리오, Log, 개발일지]

toc: true
toc_sticky: true
 
date: 2025-06-19
last_modified_at: 2025-06-19
---

# 💡 1. 진행한 작업
- SharedPreference 저장&불러오기를 리스트 형태로 변경.
- ScheduleList Recyclerview에서 아이템 클릭 시 해당 아이템이 갖고 있던 데이터로 열리도록 수정.
<br><br><br>
<!-- ---------- -->



# 💡 2. 알게 된 점
- 여러 개의 데이터들을 저장하거나 불러올 때 data class를 List 방식으로 넣어주어야 가능.
- Recyclerview를 갱신시킬 때 호출 시점이 중요하고 한 번 Adapter에 지정해준 List는 다시 Adapter에 넣어주지 않더라도 갱신 가능.
- SuppressLint 어노테이션은 특정 경고를 무시하는데 사용.
<br><br><br>
<!-- ---------- -->



# 💡 3. 트러블슈팅 & 해결 방법
- 수정을 위해 다른 Activity로 넘어가버리면 Recyclerview Adapter에 들어가있는 List가 두 곳 이상의 Activity에 존재해야 되는 문제가 있어서 이를 해결하기 위해 Activity 이동 후 Result 데이터를 받아와서 결과적으로 List는 하나의 Activity에만 존재해도 관리할 수 있도록 작성함.
<br><br><br>
<!-- ---------- -->



# 💡 4. 개선 사항
- Recyclerview 갱신에 다양한 방법이 있는데 현재는 한 개만 수정되더라도 모든 데이터들을 갱신하는 방식으로 구현해두었기 때문에 리소스 낭비가 있음. 수정이 발생된 특정 데이터만 갱신하는 방식으로 개선하면 좋을 것 같음.
<br><br><br>
<!-- ---------- -->



# 💡 5. 다음 목표
- ScheduleList Recyclerview에서 아이템 클릭 후 편집 완료 시 SharedPreference에도 변경된 데이터로 저장.
<br><br><br>
<!-- ---------- -->