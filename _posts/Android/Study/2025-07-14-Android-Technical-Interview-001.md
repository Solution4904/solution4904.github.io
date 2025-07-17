---
title:  "안드로이드 기술면접 대비 - 001"
excerpt: ""

categories:
  - android-study
tags:
  - [Android, 안드로이드, Study, 공부, Interview, 면접]

toc: true
toc_sticky: true
 
date: 2025-07-14
last_modified_at: 2025-07-14
---


# 💡 [1] 인텐트(Intent)란?
- 수행될 작업에 대한 추상적인 설명. Activity, Service, BroadcastReceiver가 통신할 수 있도록 하는 메시징 객체 역할.
	- 일반적으로 Activity 실행, Broadcast 전송, Service 시작 등에 사용
	- Component 간에 데이터 전달
	- 명시적(Explicit), 암시적(Implicit) 두 가지 유형이 존재
		- 명시적<br>
    Activity, Service 등의 Component를 직접 이름으로 지정하여 명시. Activity -> Activity 전환과 같이 대상 Component를 알고 있을 때 사용. <br>
    -> [Intent(this, TargetActivity::class.java)]
		- 암시적<br>
    특정 Component를 지정하지 않고 작업을 수행. 브라우저에서 웹 페이지를 열거나 다른 앱과 콘텐츠를 공유하는 경우 사용. <br>
    -> [intent.data = Uri.parse("https://www.exmaple.com")]


### 📑 인텐트 필터(Intent Filters)란?
- App Component가 Link를 열거나 Broadcast 처리와 같은 특정 Intent에 어떻게 응답할 수 있는지를 정의.


### 📖 Question
1. 명시적 인텐트와 암시적 인텐트의 차이점은 무엇인가요?
2. 명시적 인텐츠와 암시적 인텐트는 각각 어떨 때 사용하나요?
<br><br><br>
<!-- ---------- -->


# 💡 [2] PendingIntent란?
- 다른 앱이나 시스템 컴포넌트가 앱을 대신하여 미리 정의된 Intent를 나중에실행할 수 있는 권한을 부여하는 또 다른 종류의 Intent.
- 알림, 서비스와 상호작용 등 앱의 수명 주기를 벗어나 트리거되어야 하는 작업에 유용.
- Activity, Service, BroadcastReceiver를 실행(호출)하기 위해 생성.
- 팩토리 메소드를 사용.


### 📖 Question
1. PendingIntent란 무엇이며, 일반 Intent와 어떻게 다른가요? 어떨 때 사용하나요?
<br><br><br>
<!-- ---------- -->


# 💡 [3] Serializable vs Parcelable
- 둘 다 다른 컴포넌트(Activity, Fragment 등) 간에 데이터를 전달하는 데 사용되는 메커니즘.

|기능|Serializable|Parcelable|
|---|---|---|
|유형|표준 Java 인터페이스|안드로이드 기반 인터페이스|
|성능|리플렉션 의존으로 인해 느림|리플렉션에 의존하지 않아 빠름|
|가비지 생성|직렬화 과정에서 많은 임시 객체를 생성|임시 객체 생성을 피함|
|사용 사례|성능이 중요하지 않은 코드베이스 때 사용|성능이 중요한 안드로이드 Activity, Service 간 데이터 전달|


### 📑 Parcelable
- 객체를 직렬화하여 Parcel을 통해 전달할 수 있도록 하는 안드로이드에 특화된 인터페이스.
- Parcleable을 구현하는 객체는 Parcel에 쓰고 복원할 수 있어서 안드로이드 컴포넌트 간에 복잡한 데이터를 전달하는 데 적합.


### 📖 Question
1. Serializable과 Parcelable의 차이점은 뭔가요?
2. 일반적으로 컴포넌트 간 데이터 전달에 Parcelable이 선호되는 이유는 무엇인가요?
<br><br><br>
<!-- ---------- -->


# 💡 [4] Context?
- 앱의 환경 또는 상태를 나타냄.
- 앱 별 리소스 및 클래스에 대한 접근을 제공.

|종류|Application|Activity|Service|Broadcast|
|---|---|---|---|---|
|생명주기|앱에 연결|액티비티에 연결|서비스에 연결|브로드캐스트리시버가 호출될 때 제공|
|사용사례|독립적이고 전역적인 오래 지속되어야 하는 Context가 필요할 때=><br> - SharedPreferences나 DB와 같은 앱 전체 리소스에 접근하는경우<br>- BroadcastReceiver를 등록하는 경우|액티비티에 특정한 리소스 접근, 다른 액티비티 시작, 레이아웃 인플레이션=><br> - UI 컴포넌트를 생성 또는 업데이트 하는 경우<br> - 다른 Activity를 실행하는 경우|네트워크 작업 또는 음악 재생과 같은 백그라운드 작업|특정 브로드캐스트에 응답|


### 📑 사용 사례
- Resources 접근 (Context.getDrawable()...)
- 레이아웃 인플레이션 (Context.LayoutInflater)
- Activity 및 Service 시작 (Context.Activity(startActivity()))
- 시스템 서비스 접근 (Context.getSystemService())
- 데이터베이스 및 SharedPreferences 접근


### 📑 주의사항
- 부적절하게 사용하면 메모리 누수, 크래시, 비효율적인 리소스 처리와 같은 심각한 문제를 일으킬 수 있음.
- 생명 주기 대상보다 오래 유지하게 되면 GC가 Context 또는 관련 리소스에 대한 메모리를 회수할 수 없게 되어 메모리 누수로 이어질 수 있음.


### 📖 Question
1. 안드로이드 앱에서 올바른 유형의 Context를 사용하는 것이 왜 중요한가요?
2. Activity Context에 대해 오랜 참조를 유지하는 것은 잠재적으로 어떤 문제를 발생시킬 수 있나요?
<br><br><br>
<!-- ---------- -->