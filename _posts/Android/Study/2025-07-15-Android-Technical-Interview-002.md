---
title:  "안드로이드 기술면접 대비 - 002"
excerpt: ""

categories:
  - android-study
tags:
  - [Android, 안드로이드, Study, 공부, Interview, 면접]

toc: true
toc_sticky: true
 
date: 2025-07-15
last_modified_at: 2025-07-15
---


# 💡 [5] Application 클래스?
- 전역 앱 상태와 생명 주기를 유지하기 위한 역할.
- Activity, Service, BroadcastReceiver와 같은 다른 컴포넌트보다 가장 먼저 초기화되는 프로세스 진입점 역할.
- 앱의 전체 생명주기에 사용 가능한 Context를 제공하므로 앱 전역에 걸쳐 공유되는 리소스 및 인스턴스를 초기화하는 데 이상적.


### 📑 사용 사례
1. 전역 리소스 관리 : DB, SharedPreferences, 네트워크 클라이언트와 같은 리소스 초기화.
2. 컴포넌트 초기화: Firebase Analytics, Timber 등.
3. 의존성 주입 : Dagger, Hilt 같은 프레임워크 초기화


### 📑 주의사항
1. 초기 앱 실행 시 지연을 방지하기 위해 onCreate()에서 무거운 Task 실행 X
2. 관련 없는 로직 포함 X
3. 공유 리소스에 대해 스레드 안정성을 보장해야 함.

### 📖 Question
1. Application 클래스의 목적은 무엇인가요?
2. 생명주기 및 리소스 관리 측면에서 Activity와 어떻게 다른가요?
<br><br><br>
<!-- ---------- -->


# 💡 [6] AndroidManifest 파일?
- 안드로이드 운영 체제에 앱에 대한 필수 정보를 정의하는 구성 파일.
- 앱과 OS 간의 브릿지 역할.
- 컴포넌트, 권한, 하드웨어, 소프트웨어 기능 등을 정의.


### 📑 주요 기능
1. 컴포넌트 선언 : Activityes, Services, BroadcastReceivers, Content Providers와 같은 필수 컴포넌트를 등록. 이를 OS가 시작하거나 상호 작용하는 방법을 알 수 있도록 함.
2. 권한 : INTERNET, ACCESS_FINE_LOCATION, READ_CONTACTS와 같은 권한 부여.
3. 하드웨어 및 소프트웨어 요구 사항 : 카메라, GPS 등 앱이 의존하는 기능을 명시하여 Play Store가 요구사항을 충족하지 않는 기기를 필터링하는데 도움.
4. 앱 메타 정보 : 앱의 패키지 이름, 버전, 최소 및 대상 API 레벨, 테마, 스타일과 같은 필수 정보 제공.
5. 인텐트 필터 : 컴포넌트에 대한 필터를 정의하여 링크 열기, 콘텐츠 공유와 같이 응답할 수 있는 Intent 종류를 명시. 다른 앱이 개발자의 앱과 상호 작용할 수 있도록 함.
6. 앱 구성 및 세팅 : 메인 런처 Activity 정의, 백업 동작 구성, 테마 지정. 앱의 동작 방식과 표시 방식을 제어하는데 도움.


### 📖 Question
1. AndroidManifest의 인텐트 필터는 앱 상호 작용을 어떻게 가능하게 하나요?
2. 액티비티 클래스가 AndroidManifest에 등록되어있지 않으면 어떻게 되나요?
<br><br><br>
<!-- ---------- -->


# 💡 [7] Activity 생명주기?
- onCreate()
  - Activity 초기화, UI 컴포넌트 설정, 저장된 인스턴스 상태 복원.
  - Activity가 소멸되고 재생성되지 않는 한 생명주기 동안 단 한 번만 호출.

- onStart()
  - Activity가 사용자에게 보이지만 아직 상호 작용할 수 없는 상태.

- onResume()
  - Activity가 Foreground에 있고 사용자가 상호 작용 가능.
  - 일시 중지된 UI 업데이트, 애니메이션, 입력 리스터 재개.

- onPause()
  - 다른 Activity(Dialog 등)에 의해 부분적으로 가려질 때 호출.
  - 애니메이션, 센서 업데이트, 데이터 저장 같은 작업 시 자주 사용.

- onStop()
  - Activity가 사용자에게 보이지 않을 때 호출.
  - Activity가 중지되어 있는 동안 불필요한 리소스를 해제할 때 사용.

- onDestroy()
  - Activity가 완전히 소멸되고 메모리에서 제거되지 전에 호출
  - 남아있는 모든 리소스를 해제하기 위한 최종 메소드.
  
- onRestart()
  - Activity가 중지되었다가 다시 시작되는 경우에만 onStart() 전에 호출.


### 📑 Activity A <-> Activity B 흐름 예시
1. Activity A 실행
  - Activity A.onCreate()
  - Activity A.onStart()
  - Activity A.onResume()

2. Activity A -> Activity B 이동
  - Activity A.onPause()
  - Activity B.onCreate()
  - Activity B.onStart()
  - Activity B.onResume()
  - Activity A.onStop()

3. Activity B -> Activity A 이동
  - Activity B.onPause()
  - Activity A.onRestart()
  - Activity A.onStart()
  - Activity A.onResume()
  - Activity B.onStop()
  - Activity B.onDestroy()

### 📖 Question
1. onPause()와 onStop()의 차이점은 무엇인가요?
2. 리소스 점유율이 높은 작업을 처리하는 경우 어떤 시나리오에서 사용해야 하나요?
<br><br><br>
<!-- ---------- -->


# 💡 [8] Fragment 생명주기?
> - 연결된 부모 Activity의 생명주기와는 별도로 자체적인 생명주기를 갖음.
> - Activity 생명주기와 유사하지만 Fragment만의 고유한 콜백 메서드가 존재.

- onAttach()
  - Frament가 부모 Activity와 연결될 때 호출.

- onCreate()
  - Fragment를 초기화할 때 호출.
  - Fragment는 생성되었지만 UI는 아직 생성되지 않았음.
  - 필수 컴포넌트 초기화, 저장된 상태 복원 등에 사용.

- onCreateView()
  - Fragment의 UI가 처음으로 그려질 때 호출.
  - LayoutInflater를 사용하여 Fragment의 레이아웃을 인플레이션하는 곳.

- onViewCreated()
  - Fragment의 뷰가 생성된 후 호출.
  - UI 컴포넌트와 사용자 상호 작용 처리에 필요한 로직을 설정하는데 사용.

- onViewStateRestored()
  - Fragment의 뷰 계층이 생성.
  - 저장된 상태가 뷰에 복원된 후 호출.

- onStart()
  - Fragment가 사용자에게 보임. (Activity onStart와 동일)
  - Fragment가 활성 상태이지만 아직 Foreground에 있진 않음.

- onResume()
  - Fragment의 UI가 완전히 화면에 표시되고 사용자와 상호 작용할 수 있을 때 호출.
  - Fragment가 완전 활성 상태이며, Foreground에서 실행 중.

- onPause()
  - Fragment가 Foreground에 있지 않지만 여전히 화면에 보이는 경우 호출.
  - Fragment가 포커스를 잃기 직전이며, Foreground에 존재하지 않을 때 지속해서는 안되는 작업을 일시 중지 시켜야 함.

- onStop()
  - Fragment가 더 이상 보이지 않음.
  - 화면 밖에 있는 동안 지속해야할 필요가 없는 작업을 중지 시켜야 함.

- onSaveInstanceState()
  - Fragment가 소멸되기 전에 UI 관련 상태 데이터를 저장하여 복원할 수 있도록 호출

- onDestroyView()
  - Fragment의 뷰 계층이 제거될 떄 호출.
  - 메모리 누수를 방지하기 위해 어댑터를 지우거나 참조를 null로 만드는 등 뷰와 관련된 리소스를 정리 해야 함.

- onDestroy()
  - Fragment 자체가 소멸될 때 호출.
  - 모든 리소스를 정리 해야 함.
  - Fragment는 여전히 부모 Activity에 연결되어 있음

- onDetach()
  - Fragment가 부모 Activity와 분리됨.


### 📖 Question
1. onCreateView()와 onDestroyView()의 목적은 무엇인가요?
2. (1)의 메소드엣 뷰 관련 리소스를 올바르게 처리하는 것이 왜 중요한가요?
<br><br><br>
<!-- ---------- -->


# 💡 []
- 


### 📑


### 📖 Question
1. 
<br><br><br>
<!-- ---------- -->