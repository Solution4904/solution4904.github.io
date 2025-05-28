---
title:  "DailyUp 어플리케이션 구상안"
excerpt: ""

categories:
  - android-portfolio
tags:
  - [Android, 안드로이드, Portfolio, 포트폴리오]

toc: true
toc_sticky: true
 
date: 2025-05-28
last_modified_at: 2025-05-28
---

# 💡 0. 수정 내역
- 2025-05-28 작성

<br><br><br>

# 💡 1. 컨셉
- 기본적인 토대는 TODO LIST 앱과 유사.
- 반복적으로 수행할 일정을 등록/관리.
- 등록되어 있는 각 일정들의 성취율을 통계로 확인.
- 체크박스 방식으로 두 가지 상태 뿐 아니라 계획했던 일정을 얼마나 수행했는지까지 체크할 수 있는 기능. (ex. '물 2L 마시기'일 때, 1L 혹은 1.5L로 체크)

<br><br><br>

# 💡 2. 예상 사용 기능 및 API
- 로컬 저장 방식
- 로컬 계정
- MVVM 패턴
- XML
- 일정 통계 (Text)

<br><br><br>

# 💡 3. 구현할 기능
- 일정 등록/삭제/수정
- 일정 달성 체크

<br><br><br>

# 💡 4. 희망 업그레이드
- 로컬 저장 방식 -> Firebase로 서버 저장 or 데이터 내보내기/불러오기
- 로컬 계정 -> 이메일 가입 or SNS연동
- Jetpack Compose 혼용
- 통계 그래프
- 기기 테마 반영 (Light / Dark)