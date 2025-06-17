---
title:  "DailyUp 어플리케이션 개발 - 002"
excerpt: ""

categories:
  - android-log
tags:
  - [Android, 안드로이드, Portfolio, 포트폴리오, Log, 개발일지]

toc: true
toc_sticky: true
 
date: 2025-06-17
last_modified_at: 2025-06-17
---

# 💡 1. 진행한 작업
- Schedule을 작성하고 Shared Preference를 사용하여 로컬 데이터 상에 저장.
- Schedule List를 표현해주는 Recyclerview에서 Item을 클릭했을 때 해당 Schedule의 데이터를 편집할 수 있도록 화면을 이동.
- Schedule Data를 Shared Preference로 저장할 수 있도록 Gson을 사용해서 Serialization/Deserialization.
- Shared Preference를 어디서든 호출하여 사용할 수 있도록 Application 단에서 초기화.
<br><br><br>
<!-- ---------- -->



# 💡 2. 알게 된 점
- 데이터를 Serialization/Deserialization 하려면 Json 문자열을 사용는데 이를 Google에서 Gson이라는 이름의 라이브러리로 제공하고 있다.
- Kotlin에선 데이터를 Serialization/Deserialization 할 때, Gson 혹은 kotlinx.serializationd을 대표적으로 사용하고 있다.
- Gson은 범용적으로 사용할 수 있으나 코틀린의 기본 값과 Null-Safety를 완벽히 지원하지 않고, kotlinx.serialization는 JetBrain에서 제공하는 공식 라이브러리여서 코틀린의 언어 특성을 잘 반영한다.
<br><br><br>
<!-- ---------- -->



# 💡 3. 트러블슈팅 & 해결 방법
- Shared Preference는 기본 타입만 지원하기 때문에 Model로 사용하고 있는 Data Class를 저장/불러오기 위해 Serialization/Deserialization 시킴.
<br><br><br>
<!-- ---------- -->



# 💡 4. 개선 사항
- Schedule List를 표시하고 있는 Recyclerview에서 Item을 클릭했을 때 수정화면으로 가서 데이터들을 초기화 하는 방식이 현재는 클릭한 Item에 이벤트를 걸어서 id 값을 Intent.PutExtra()로 전달해서 Shared Preference에 동일한 id 값을 가진 데이터를 찾아내는 방식으로 구현해두었는데, Intent.PutExtra()할 때 Data Class를 사용 중이라 Serialization/Deserialization 과정이 들어가있는데 이를 Pacelable을 사용하면 Data Class를 그대로 사용할 수 있다고 함. 지금은 클래식하게 구현하려는 목적이여서 사용하지 않았음.
<br><br><br>
<!-- ---------- -->



# 💡 5. 다음 목표
- Schedule List를 표시하고 있는 Recyclerview에서 Item을 클릭했을 때 수정화면에 id 값을 기준으로 일치하는 데이터들을 가져와서 초기화.
- Schedule List들을 List로 묶어서 하나의 Key 값 데이터로 Shared Preference에 저장되도록 수정.
- 저장되어 있는 Shared Preference 로컬 데이터가 있을 경우 해당 데이터들로 Schedule List Recyclerview에 표시되도록 구현.
<br><br><br>
<!-- ---------- -->