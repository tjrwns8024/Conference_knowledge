# Android Studio Build Talk 

#### 안드로이드 빌드: 설탕 없는 세계 ( 카카오 뱅크 김용욱)

-  Post Compliation 를 메인으로 다룬다
- Desugar: 개발자를 위한 편의 를 빌드 과정에서 제거하는 것

##### 후처리를 알면 도움 되는 점

- 보안을 강화 할 수 있다
- 언어의 한계를 극복할 수 있다
- APT의 한계 극복 가능
- 반복적인 작업 에 도움

##### android build 의 특수성

- Java VM은 스택기반의 VM

- 32비트 기반의 스택

- 상수의 종류 구별 x

  (Dex)

  64k 메서드 단위로 여러 클래스가 하나의 파일에 합쳐져 있음

  상수들은 같은 DEX에서 공유함

  달빅 바이트 코드를 사용

  상대 주소 사용 -> 공간 효율 

  (Jack & Jill)

  한번에 DEX로 가는 툴체인 -> 생태계가 호환되지 않는 문제

  

##### android build 과정

- 그래들 플러그인

  1. 프로퍼티 파일에 지정된 플러그인 을 실행
  2. Entry 메서드인 apply 메서드를실행
  3. 트랜스폼과 환경 설정

- Task Manager

  1. createPostCompilation Tasks

     여러 트랜스폼을 호출하여 후처리

     인터널 트랜스폼 간 호출 순서 정해짐

     써드파티 트랜스폼 간 순서 보장 x

- Transform 설정

  이름 , 입/출력의 유형을 정의

##### 구글이 만든 트랜스폼

- ShrinkResourcesTransform

  사용하지 않는 리소스 제거

- DesugarTransform

  문법 설탕등을 제거

  DESUGAR_MAIN을 통해 람다 등의 코드 변형

- Proguard Transform

  난독화를 위한 트랜스폼

  Proguard 객체에게 난독화를 요청

  

  ### 정리

  - 안드로이드빌드과정의특이성과흐름을배웠습니다. 

  

  #### R고 써야 뒷탈 없는 R8( LINE + 차영호)

  - D8 & R8
  - Proguard Rules
  - How to track issuses of R8
  - Case studies

  

  ###### D8

  -> dexer that converts java byte code to dex code

  -> replacement for teh DX dexer

  -> D8 supports desugaring  (Since android studio 3.2)

   	- 언어에 대한 기능 제공
   	- java8 API 는 제공하지 않는다

  

  ###### R8

  -> java program shrinking and minification tool that converts gava byte coe to optimized dex code.

  (android 3.4 )부터는 기본값

  

  ** Proguard support will be removed soon.. 

  

  ###### Sources of Proguard Rules

  - Application  
  - Andoird Gradle Plugin
  - Libraries
  - AAPT

  


  ### 앱 모듈화와 비드 최적화 ( 쿠팡 김필우)

  - AGP(Android Gradle Plug in)

  - DIP(Dependency Inversion Principle)

    Layered Architecture

    하위 계층의 레이어가  상위 계층 레이어의 기능을 원할때 

  - PBL(Package By layer)

    layer 별로 패키지 구성

  - PBF(Package by Feature)

  

  피러 패키징 과 ㅡMVP 패턴의 적용 예시

  - Login 이라는 피처 패키지를 생성한다고 가정하자. model presenter , view , util 이라는 서브 패키지들을 굿어 할 수 있다.

  ###### 모듈화

  - 관심사 분리의 물리적 제약 적용 버전

  ####  빌드 최적화

  1. 프로파일링(profiling)

  2. Build optimization tips

     - use lastest Android Gragle Plugin 
     - Avoid legacy multidex
     - Avoid inadvertent changes
     - use Gradle cache

  3. multiidex ( Avoid legacy multidex)

     - sdk version 21 을 기준으로 multidex를 만드느 채스크의 종류가 달라짐

  4. fabric(7. Avoid inadvertent changes)

  5. cache(10. use Gradle cache)

  6. Task Graph flattening

     

  오직 소스 변경이 있는 모듈만 lint 체크

  