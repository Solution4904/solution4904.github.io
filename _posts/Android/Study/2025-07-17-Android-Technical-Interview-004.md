---
title:  "안드로이드 기술면접 대비 - 004"
excerpt: ""

categories:
  - android-study
tags:
  - [Android, 안드로이드, Study, 공부, Interview, 면접]

toc: true
toc_sticky: true
 
date: 2025-07-17
last_modified_at: 2025-07-17
---


# 💡 [11] ContentProvider란?
- 구조화된 데이터에 대한 접근을 관리하고 앱 간 데이터 공유를 위한 표준화된 인터페이스를 제공하는 컴포넌트.
- 다른 앱이나 컴포넌트가 데이터를 쿼리, 삽입, 업데이트, 삭제하는 데 사용할 수 있는 중앙 저장소 역할.
- 앱 간의 안전하고 일관된 데이터 공유 보장
- 여러 앱이 동일한 데이터에 접근해야 하거나 데이터베이스 또는 내부 저장소 구조를 노출하지 않고 다른 앱에 데이터를 제공하려는 경우 유용.


### 📑 목적
- 데이터 접근 로직을 캡슐화하여 앱 간 데이터 공유를 더 쉽고 안전하게 만드는 것.


### 📑 주요 구성 요소
1. 권한 : ContentProvider를 식별.
2. Path : 데이터 유형 지정.
3. ID : 데이터 셋 내의 특정 항목을 참조.


### 📑 사용 사례
- 다른 앱 간 데이터 공유.
- 앱 시작 시 컴포넌트 또는 리소스 초기화.
- 연락처, 미디어 파일, 앱 별 데이터와 같은 구조화된 데이터에 대한 접근 제공.
- 연락처 앱이나 파일 선택기와 같은 안드로이드 시스템 기능과의 통합 활성화.
- 세분화된 보안 제어를 통한 데이터 접근 허용.


### 📖 Question
1. ContentProvider URI의 주요 구성 요소는 무엇인가요?
2. ContentResolver는 데이터를 쿼리하거나 수정하기 위해 ContentProvider와 어떻게 상호작용 하나요?
<br><br><br>
<!-- ---------- -->


# 💡 [12] 구성 변경을 어떻게 처리하나요?
- 화면 회전, 언어 변경, 다크/라이트 모드 전환, 글꼴 크기/두께 조정과 같은 설정 값이 변경되었을 때 원활한 사용자 경험을 유지하는데 중요한 역할.
- 기본적으로 안드로이드 시스템은 구성 변경이 발생할 때 Activity를 다시 시작하며 이로 인해 일시적으로 UI의 상태가 손실될 수 있음.


### 📑 구성 변경에 대응하는 방법
1. UI 상태 저장 및 복원 : onSaveInstanceState() 및 onRestoreInstanceState() 메소드를 구현하여 Activity 재생성 중 UI 상태를 보존하고 복원.
2. Jetpack ViewModel : ViewModel 객체는 Activity 재시작 범위를 넘어서 존재하도록 설계되어있으므로, 구성 변경에도 유지되어야 하는 UI 관련 데이터를 저장, 복원하는데 이상적.
3. 구성 변경 수동으로 처리 : AndroidManifest에서 Activity가 처리할 구성 변경 사항을 android:configChanges 속성을 사용하여 선언, 이후 Activity에서 onConfigurationChanged() 메소드를 재정의 하여 수동으로 관리.
4. Jetpack Compose의 rememberSaveable 활용 : onSaveInstanceState()와 유사하게 작동.


### 📖 Question
1. 구성 변경을 처리하기 위한 전략에는 무엇이 있나요?
2. ViewModel은 구성 변경으로부터 손실될 수 있는 UI 관련 데이터를 어떻게 보존하나요?
3. AndroidManifest 파일에서 aindroid:configChanges 속성은 Activity 생명주기와 동작에 어떤 영향을 미치나요?
4. Activity 재시작에 의존하는 것이 아니라 onCinfigurationChagned() 메소드를 사용해야하는 시나리오의 예시를 들어주세요.
<br><br><br>
<!-- ---------- -->


# 💡 [13] 안드로이드에서 효율적인 메모리 관리 방법과 메모리 누수를 어떻게 방지하는가?
- 사용되지 않는 메모리를 자동으로 회수하여 활성 중인 앱 및 서비스에게 효율적인 메모리 할당을 보장하는 가비지 컬렉션 메커니즘을 통해 메모리를 관리.


### 📑 메모리 누수의 원인
- 앱이 더 이상 필요하지 않은 객체에 대한 참조를 유지하여 가비지 컬렉터가 메모리를 회수하지 못하게 할 때 발생.
- 일반적으로 부적절한 생명주기 관리, 정적 참조/Context에 대한 장기 참조 유지 등이 원인


### 📑 메모리 누수를 피하는 모범 사례
1. 생명주기를 인지하는 컴포넌트 사용 : ViewModel, Flow, LiveData와 같은 생명주기를 인지하는 컴포넌트를 활용하면 관련 생명주기가 끝날 때 리소스가 적절하게 해제됨.
2. Context에 대한 오랜 참조 피하기 : 정적 필드나 싱글톤과 같은 오래 지속되는 객체에서 Activity 또는 Context에 대한 참조를 유지하지 않을 것. 만약 장기적인 참조가 필요하다면 Activity나 Fragment의 생명주기와는 독립적인 ApplicationContext를 사용할 것.
3. 리스너 및 콜백 등록을 올바르게 해제 : 항상 적절한 생명주기 메소드에서 리스너, 관찰자, 콜백을 올바르게 등록/해제할 것.
4. 중요하지 않은 객체는 WeakReference 사용 : 강력한 참조가 필요하거나 장기적으로 참조가 보장되어야 하는 객체가 아니라면 WeakReference 사용. 이는 메모리가 필요할 때 가비지 컬렉터가 해당 객체를 언제든지 회수할 수 있음.
5. 누수 감지 툴 사용 : LeakCanary와 같은 툴 활용. 혹은 Android Studio의 Memory Profiler 사용.
6. View에 대한 정적 참조 피하기 : View는 Activity Context에 대한 참조를 유지함으로서 메모리 누수를 유발할 수 있음.
7. 리소스 닫기 : 파일 스트림, Cursor, 데이터베이스 연결과 같은 리소스는 더이 상 필요하지 않을 때 항상 명시적으로 해제할 것.
8. Fragment와 Activity 현명하게 사용하기 : Fragment를 과도하게 사용하거나 부적절하게 참조를 유지하지 말 것. OnDestroyView() 또는 onDetach()에서 Fragment 참조를 정리.


### 📖 Question
1. 앱에서 메모리 누수의 일반적인 원인은 무엇이며, 이를 사전에 방지하기 위한 방법에는 어떤 것들이 있나요?
2. 안드로이드의 가비지 컬렉션 메커니즘은 어떻게 작동하며, 개발자는 앱에서 메모리 누수를 감지하고 수정하기 위해 어떤 방법을 사용할 수 있나요?
<br><br><br>
<!-- ---------- -->


# 💡 [14] ANR
- ANR(Application Not Responding)은 앱의 메인 스레드(UI Thread)가 오랫동안(통상 5초) 차단될 때 발생하는 안드로이드 시스템 오류.


### 📑 주요 원인
- 메인 스레드(UI)에서 5초 이상 걸리는 무거운 작업
- 장시간 실행되는 네트워크, 데이터베이스 등의 I/O 작업
- UI 스레드 차단 작업 (UI 스레드에서의 동기 작업 등)


### 📑 예방 방법
1. 무거운 작업을 메인 스레드 밖으로 이동 : 파일 I/O, 네트워크 요청, 데이터베이스 쿼리 등과 같은 무거운 작업은 백그라운드 스레드 사용. (AsyncTask, Executors, Thread, Kotlin Coroutines Dispatchers.IO)
2. WorkManager 사용 : 데이터 동기화 같은 장기적인 작업에 사용. WorkManager는 개발자가 필요한 작업을 사전에 스케쥴링하고 메인 스레드 외부에서 실행되도록 보장.
3. 데이터 불러오기 최적화 : Paging을 구현하여 데이터를 작고 관리 가능한 청크로 가져와 UI 과부하를 방지하고 성능을 향상.
4. 구성 변경 시 UI 작업 최소화 : ViewModel을 활용해 UI 관련 데이터를 유지하고 화면 회전과 같은 구성 변경 중에 불필요한 UI 렌더링 피하기.
5. Android Studio Profiler 사용 : 성능 병목 현상을 식별하고 해결하기.
6. Blocking 호출 피하기 : 긴 루프, sleep 호출, 네트워크 요청을 동기로 수행.
7. Handler 사용 : 응답성 있는 UX을 위해 Thread.sleep() 대신 Handler.postDelayed()를 사용하여 지연 작업 처리 가능.


### 📖 Question
1. ANR을 진달하고 앱 성능과 UX 개선해본 경험이 있나요?
<br><br><br>
<!-- ---------- -->


# 💡 [15] 딥 링크(Deep links)?
- 사용자가 URL이나 알림과 같은 외부 소스에서 앱 내의 특정 화면이나 기능으로 직접 이동할 수 있도록 함.


### 📑 정의 방법
1. AndroidManifest에서 intent filter 선언
2. Activity에서 딥 링크 처리
3. 딥 링크 테스트 (adb 명령어로 가능)


### 📑 추가 고려 사항


### 📖 Question
1. 


<br><br><br>
<!-- ---------- -->


# 💡 [14] ANR
- ANR(Application Not Responding)은 앱의 메인 스레드(UI Thread)가 오랫동안(통상 5초) 차단될 때 발생하는 안드로이드 시스템 오류.


### 📑 주요 원인
- 메인 스레드(UI)에서 5초 이상 걸리는 무거운 작업
- 장시간 실행되는 네트워크, 데이터베이스 등의 I/O 작업
- UI 스레드 차단 작업 (UI 스레드에서의 동기 작업 등)


### 📑 예방 방법
1. 무거운 작업을 메인 스레드 밖으로 이동 : 파일 I/O, 네트워크 요청, 데이터베이스 쿼리 등과 같은 무거운 작업은 백그라운드 스레드 사용. (AsyncTask, Executors, Thread, Kotlin Coroutines Dispatchers.IO)
2. WorkManager 사용 : 데이터 동기화 같은 장기적인 작업에 사용. WorkManager는 개발자가 필요한 작업을 사전에 스케쥴링하고 메인 스레드 외부에서 실행되도록 보장.
3. 데이터 불러오기 최적화 : Paging을 구현하여 데이터를 작고 관리 가능한 청크로 가져와 UI 과부하를 방지하고 성능을 향상.
4. 구성 변경 시 UI 작업 최소화 : ViewModel을 활용해 UI 관련 데이터를 유지하고 화면 회전과 같은 구성 변경 중에 불필요한 UI 렌더링 피하기.
5. Android Studio Profiler 사용 : 성능 병목 현상을 식별하고 해결하기.
6. Blocking 호출 피하기 : 긴 루프, sleep 호출, 네트워크 요청을 동기로 수행.
7. Handler 사용 : 응답성 있는 UX을 위해 Thread.sleep() 대신 Handler.postDelayed()를 사용하여 지연 작업 처리 가능.


### 📖 Question
1. ANR을 진달하고 앱 성능과 UX 개선해본 경험이 있나요?
<br><br><br>
<!-- ---------- -->


# 💡 [15] 딥 링크(Deep links)?
- 사용자가 URL이나 알림과 같은 외부 소스에서 앱 내의 특정 화면이나 기능으로 직접 이동할 수 있도록 함.


### 📑 정의 방법
1. AndroidManifest에서 intent filter 선언
2. Activity에서 딥 링크 처리
3. 딥 링크 테스트 (adb 명령어로 가능)


### 📑 추가 고려 사항
- 커스텀 스키마 : 앱 내부 적으로 실행하는 링크에 대해서 사용 가능. 경우에 따라 호환성을 위해 HTTP(S) URL을 선호하기도 함.
- 내비게이션 : 딥 링크 데이터를 기반으로 앱 내의 다른 Activity나 Fragment로 이동하기 위해 Intent 사용
- 폴백 처리(Fallback Handling) : 앱이 딥 링크 데이터가 유효하지 않거나 불완전한 경우를 처리.
- App Links : HTTP(S) 딥 링크가 브라우저 대신 앱에서 직접 열리도록 함.


### 📖 Question
1. 안드로이드에서 딥링크를 어떻게 테스트 하나요?
2. 다양한 기기와 시나리오에서 올바르게 작동하는지 확인하기 위해 사용하는 디버깅 기법이 있나요?
<br><br><br>
<!-- ---------- -->