---
title:  "DailyUp 어플리케이션 개발 - 015"
excerpt: ""

categories:
  - android-log
tags:
  - [Android, 안드로이드, Portfolio, 포트폴리오, Log, 개발일지]

toc: true
toc_sticky: true
 
date: 2025-09-20
last_modified_at: 2025-09-20
---

# 💡 1. 진행한 작업
- MVVM 아키텍처를 위한 Observer, Event Flow 이어서 적용.
<br><br><br>
<!-- ---------- -->



# 💡 2. 알게 된 점
- Two-Way Binding이 불가능한 타입의 값이 존재할 수도 있다. 실제 값은 Int지만 입력하는 EditText는 String으로 들어가므로 오류가 발생한다.
<br><br><br>
<!-- ---------- -->



# 💡 3. 트러블슈팅 & 해결 방법
- xml과 양방향 데이터 바인딩을 시도하다가 정확한 방법을 알지 못해서 단방향 데이터 바인딩으로 구현하고 있었는데, 작업 완료 후 빌드를 해봤는데 작업한 기능을 실행시켜보니 앱이 죽어버리는 문제가 발생했다. Logcat으로 확인해봤지만 xml에서 발생한 오류여서 StackTrace로도 정확히 어디에서 어떤 걸로 발생되고 있는 문제인지 알 수가 없었다. 결국 작업했던 모든 것들과 관련된 정보들을 조사하다가 문제 부분을 발견했다. xml에서 editText View의 text 속성 값으로 viewModel의 값을 바인딩해두었었는데, 바인딩되어 있는 값이 String 타입이 아닐 경우 발생하는 문제였다. 오류도 안뜨고 별 생각 없이 숫자->문자는 캐스팅될 거라고 생각했다.
- xml에 editText에 text 속성 값을 데이터바인딩으로 초기화 시키면서 toString(), 혹은 Int.Parse()로 변환시키려고 알아보니 import로 Integer와 String을 추가해서 사용해야 한다는 걸 알아냈다. 그래서 문제 없이 추가하고 빌드해봤지만 Missing import expression although it is registered 라는 로그와 함께 빌드가 되질 않았다. 표현식이 누락되었다는데 무슨 뜻인지를 모르겠어서 여기저기 알아보니 import 하지 않아도 기본적으로 사용할 수 있는 상태인데 중복으로 import 시킬 경우 발생된다는 글을 보고, import를 지워보니 정상적으로 빌드할 수 있었다. 다만 분명히 import 시키기 전에는 정의되지 않았다고 xml에 적어넣어도 사용할 수 없었는데 왜 동일한 상태에서 갑자기 정상적으로 사용 가능한건지 모르겠다.(버그인가?)
<br><br><br>
<!-- ---------- -->



# 💡 4. 개선이 필요한 사항
- 
<br><br><br>
<!-- ---------- -->



# 💡 5. 다음 목표
- 메인 일정 리스트가 한개만 표시되고 있는 문제 수정.
- MVVM 아키텍처를 위한 Observer, Event Flow 이어서 적용.
<br><br><br>
<!-- ---------- -->