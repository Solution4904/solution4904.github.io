---
title:  "DailyUp 어플리케이션 개발 - 030"
excerpt: ""

categories:
  - android-log
tags:
  - [Android, 안드로이드, Portfolio, 포트폴리오, Log, 개발일지]

toc: true
toc_sticky: true
 
date: 2026-06-24
last_modified_at: 2026-06-24
---

# 💡 1. 진행한 작업
- RecyclerView.Adapter -> ListView.Apdater 수정.
- DiffUtil 사용으로 NotifyDataSetChanged 어노테이션 제거.
- 스레드 별 작업 분산으로 인한 빌드 에러 수정.
- 일정 클릭 관련 이벤트 처리를 View에서 ViewModel로 이전.
<br><br><br>
<!-- ---------- -->



# 💡 2. 알게 된 점
- 지정한 최대값보다 크면 최댓값을 반환하고, 작거나 같으면 그대로 반환하는 coerceAtMost() 사용해봄. Math.min(value, max)와 동일한 역할을 하지만 메소드 체이닝 시 가독성이 좋음.
- 두 리스트의 차이를 계산하여 변경된 부분만 효율적을 업데이트 해주는 유틸리티 클래스 DiffUtil 사용해봄. RecyclerView에서 데이터가 바뀔 때 전체 리스트를 다시 그리는 notifyDataSetChanged()의 비효율성을 개선.
- RycyclerView의 Adapter는 RecyclerView Adapter가 아니어도 됨. DiffUtil을 이미 내장하고 있는 ListAdapter가 추천된다고 함. ListAdapter는 RecyclerView.Adapter를 상속받은 추상 클래스이기 때문에 사용 가능.
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
- 코드 정리, 리팩토링, 개선
<br><br><br>
<!-- ---------- -->