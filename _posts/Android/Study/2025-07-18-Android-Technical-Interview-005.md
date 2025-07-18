---
title:  "안드로이드 기술면접 대비 - 005"
excerpt: ""

categories:
  - android-study
tags:
  - [Android, 안드로이드, Study, 공부, Interview, 면접]

toc: true
toc_sticky: true
 
date: 2025-07-18
last_modified_at: 2025-07-18
---


# 💡 [16] Tasks? Back Stack?
> - Task<br>
>   - 사용자가 특정 목표를 달성하기 위해 상호 작용하는 Activity의 집합.
>   - 일반적으로 Launcher나 Intent를 통해 Activity가 실행될 때 시작.
>   - Back Stack으로 구성되며 후입선출(LIFO) 구조로 이루어져 있음.
>   - Intent 및 Activity Luanch mode가 어떻게 구성되었는지에 따라 여러 앱과 해당 Activity에 속해 있을 수 있음.

> - Back Stack<br>
>   - 태스크 내 Activity의 기록을 유지.
>   - 사용자가 새 Activity로 이동하면 현재 Activity가 스택에 Push되고, 뒤로 가기 버튼을 누르면 스택의 맨 위 Activity가 Pop되어 그 아래에 있던 Activity가 재개.
>   - Activity Launch Mode와 Intent Flags의 영향을 받음.


### 📑 사용 사례
- Launch Mode : 주로 AndroidManifest 파일의 \<activity> 태그 아래에 선언. 개발자가 Activity의 기본 동작을 설정할 수 있도록 함.
- Intent Flags : Intent를 생성할 때 개발자가 유동적으로 플래그를 설정.


### 📖 Question
1. singleTask와 singleInstance의 차이는 무엇이고, 각각 어떤 시나리오에서 사용해야 하나요?
2. Activity Launch Modㄷ는 어떤 타입이 존재하며, Task와 Back Stack 동작에 어떤 영향을 미치나요?
<br><br><br>
<!-- ---------- -->


# 💡 [17] Bundle
- Activity, Fragment, Service와 같은 컴포넌트 간에 데이터를 전달하는데 사용되는 키-값 쌍 데이터 구조.
- 일반적으로 앱 내에서 작은 용량의 데이터를 효율적으로 전송하는데 사용.


### 📑 일반적인 사용 사례
- Activity 간 데이터 전달.
- Fragment 간 데이터 전달.
- Instance 상태 저장 및 복원 (onSaveInstanceState(), onRestoreInstanceState())
- Service에 데이터 전달


### 📖 Question
1. 구성 변경 중 onSaveInstanceState()는 UI 상태를 보존하기 위해 Bundle을 어떻게 활용하며, Bundle에 어떤 유형의 데이터를 담을 수 있나요?
<br><br><br>
<!-- ---------- -->


# 💡 [18] Activity/Fragment 간의 데이터 전달
- Activity 간 데이터 전달
  - Intent
- Fragment 간 데이터 전달
  - Bundle
  - Jetpack Navigation 라이브러리 (런타임 시 값을 안전하게 가져올 수 있음)
  - Shared ViewModel (Fragment간의 의존성을 피하고, Fragment의 생명주기에 따라 안전하게 데이터 수신 가능)


### 📖 Question
1. 동일한 Activity 내에서 Fragment 간 데이터를 주고받을 때 어떤 방법이 효과적인가요?
2. ViewModel을 활용한다면 Bundle이나 직접적인 Fragment 트랜잭션을 사용하는 것과 비교했을 때 어떤 이점이 있나요?
<br><br><br>
<!-- ---------- -->


# 💡 [19] 구성 변경 시 Activity의 변화
1. Activity 종료 및 재시작 : Activity.onPause() -> Activity.onStop() -> Activity.onDestroy() 호출 이후 onCreate()로 재시작.
2. 리소스 리로딩 : 레이아웃, 드로어블, 문자열 등을 리로딩해서 앱이 화면 방향, 테마, 언어와 같은 변경 사항이 반영되도록 함.
3. 데이터 손실 방지 : onSaveInstanceState()/onRestoreInstanceState(), ViewModel 등으로 인스턴스 상태를 저장/복원.


### 📑 재생성을 유발하는 구성 변경
1. 화면 회전 (가로/세로 회전)
2. 테마 변경 (다크/라이트 모드)
3. 글꼴/크기 변경
4. 언어 변경


### 📑 재생성 피하기
- androidmanifest에서 android:configChanges 속성을 추가함으로서 변경 사항을 개발자가 수동적으로 처리하는 형태로 책임을 위임.

### 📖 Question
1. 구성 변경으로 인한 Activity 재생성으로 인한 데이터 손실과 복원 및 보존, UI 상태 복구를 어떻게 하나요?
<br><br><br>
<!-- ---------- -->


# 💡 [20] ActivityManager
- 기기에서 실행 중인 Activity, Task, Preocess에 대한 정보를 제공하고 관리하는 안드로이드 시스템 서비스.


### 📑 주요 기능
1. Task 및 Activity 정보 : 실행 중인 Task, Activity 및 스택 상태에 대한 세부 정보 추적 가능.
2. 메모리 관리 : 시스템 전체의 메모리 사용량에 대한 정보 제공.
3. 앱 프로세스 관리 : 실행 중인 앱 프로세스 및 Service에 대한 세부 정보 쿼리 가능.
4. 디버깅 및 진단 : 힙 덤프 생성, 앱 프로파일링과 같은 디버깅 도구를 제공.


### 📑 활용 사례
- Block이라는 기업에서 관리하는 LeakCanary라는 안드로이드 앱용 오픈 소스 메모리 누수 감지 라이브러리에서 내부적으로 메모리 상태 및 정보 추적을 위해 ActivityManager 활용.

### 📖 Question
1. ActivityManager.getMemoryInfo()를 어떻게 앱 성능 최적화에 활용할 수 있나요?
2. 시스템이 메모리 부족 상태에 들어가면 개발자는 어떤 조치를 취해야하나요?
<br><br><br>
<!-- ---------- -->


# 💡 [21] SparseArray
- HashMap과 유사하게 정수 키를 객체 값에 매핑하는 안드로이드에 최적화된 데이터 구조.
- Map이나 HashMap보다 메모리 관리 측면에서 효율적이고 상황에 따라 성능이 더 좋음.


### 📑 주요 특징
1. 메모리 효율성 : 키-값 매핑을 위해 HashTable을 사용하는 HashMap과 달리 오토박싱(int->Interger 변환)을 피하고 Entry 객체와 같은 추가 데이터 구조에 의존하지 않음. 이로 인해 훨씬 적은 메모리 소비.
2. 성능 : 매우 큰 데이터 셋의 경우 HashMap만큼 빠르진 않지만, 메모리 최적화로 중간 크기의 데이터 셋에서 더 나은 성능 제공
3. Null 키 값 사용 불가 : 키 값으로 기본 정수를 사용하므로 Null 불허.


### 📑 사용 이점
1. 오토박싱 방지 : Entry 객체와 같은 추가 데이터 구조에 의존하지 않기 때문에 박싱/언박싱과정이 없어서 메모리와 계산 작업 절약.
2. 메모리 절약 : Entry와 같은 여러 객체를 생성하는 HashMap과 달리 내부적으로 기본 배열을 사용하기 때문에 메모리 차지 공간이 줆.
3. 컴팩트한 데이터 저장에 효율적
4. 안드로이드 구조에 특화


### 📑 한계
1. 성능 트레이드오프 : 키 조회를 위해 이진 탐색을 사용하기 때문에 매우 큰 데이터 셋의 경우 HashMap보다 느림.
2. 정수 키만 사용 가능 : 정수 키로 제한되어 다른 유형의 키가 필요한 사용 사례에는 부적합.


### 📖 Question
1. HashMap 대신 SparseArray를 사용하는 건 어떤 경우에 효율적인가요?
2. 성능 및 사용성 측면에서 트레이드오프는 무엇인가요?
<br><br><br>
<!-- ---------- -->


# 💡 [22] 런타임 권한 처리
- 안드로이드 6.0(API 23)부터 앱 설치 시 자동으로 권한을 획득하는 대신 런타임 위험 권한을 명시적으로 요청해야 함.


### 📑 권한 선언 및 확인
- AndroidManifest에 권한 선언.
- 런타임 시에 사용자가 해당 권한이 필요한 기능과 상호 작용할 때만 권한 요청.


### 📖 Question
1. 안드로이드의 런타임 권한 시스템은 사용자 개인 정보를 어떻게 보호하나요?
2. 민감한 권한을 요청하기 전에 앱은 어떤 시나리오를 고려해야 하나요?
<br><br><br>
<!-- ---------- -->