# ZeroRange

Photon Fusion 기반 멀티플레이 FPS 게임 프로젝트입니다.

---

## 1. 프로젝트 소개 

ZeroRange는 Unity 및 Photon Fusion을 이용하여 개발한 멀티플레이 FPS 게임 프로젝트입니다.
Firebase Auth 로그인/회원가입, 팀 선택, 투척물 시스템, 줌 기능, 맵 구성 등 기본적인 FPS 플레이 흐름을 포함하고 있습니다.
국민대학교 2025년 2학기 게임소프트웨어 팀 프로젝트로 진행하였습니다.

---

## 소스 코드 관리 

본 프로젝트의 전체 소스는 GitHub가 아닌 Unity Version Control(UVC, Plastic SCM)을 통해 관리합니다.
GitHub 저장소에는 문서 및 일부 공개 가능한 파일만 포함되며, 실제 개발 소스는 UVC를 통해 내려받아야 합니다.

* 개발 참여자는 UVC Workspace에서 프로젝트를 Pull하여 사용합니다.
* Unity Editor의 Version Control(Plastic SCM) 패널을 통해 변경 사항을 관리합니다.
* GitHub 저장소만 다운로드할 경우 전체 소스가 포함되지 않아 실행이 불가능할 수 있습니다.

---

## 2. 주요 기능 

* 멀티플레이 네트워크 FPS (Photon Fusion 기반)
* 투척물(수류탄) 시스템
* 플레이어 카메라 줌 및 시야 로직
* 팀 로직 및 점수판 UI
* Firebase 로그인 및 사용자 인증
* 기본 맵 구현 및 스폰 포인트 관리
* 총기 반동 시스템
* 클래스(역할) 시스템

---

## 3. 설치 방법 

### 요구 사항

* Unity 2022.3.62f2
  (기존 2022.3.62f1을 사용하였으나 보안 이슈로 인해 f2 버전으로 업그레이드하여 개발하였습니다.)
* Photon Fusion SDK
* Firebase SDK for Unity

---

### 설치 절차 

Unity Editor에서 프로젝트를 직접 실행하거나 수정하려면 다음 절차를 수행합니다.

```
1. UVC(Plastic SCM)에서 전체 소스를 Pull합니다.
2. Unity Hub에서 Unity 2022.3.62f2 버전으로 프로젝트를 엽니다.
3. Photon Fusion App ID를 등록합니다.
4. Firebase Authentication 설정을 구성합니다.
5. Play Mode 또는 Build를 통해 실행합니다.
```
!! 현재 UVC유료구독 해지 이슈로 인해서 권한 문제로 인해 에디터에서 실행이 불가한것을 확인했습니다.!!
!! 실제로 게임을 실행할 때는 Build.zip파일을 압축해제한 후 Build/Game_Software.exe 를 실행해주시면 감사하겠습니다. !!
---

### 빌드된 실행 파일(.exe)로 플레이하는 경우

빌드된 실행 파일로 실행할 경우에는 **위 절차가 필요하지 않습니다.**
로그인 이후 바로 게임을 이용할 수 있습니다.

---

## 4. 실행 방법 

### 로그인 정보 (테스트 계정)

```
Email: test@gmail.com
Password: 123456
```

---

### 실행 흐름

```
Login Scene → StartUp Scene → DeathMatch Scene
```

### Login Scene

테스트계정을 이용하여 로그인 하거나, Signup버튼을 클릭하여 회원가입할 수 있습니다.
로그인이 성공하면 StartUp Scene으로 이동합니다.

### StartUp Scene

Quick Play버튼을 클릭하여  DeathMatch Scene으로 이동할 수 있습니다. 현재 열려있는 Gameroom이 없다면 Host로 방을 열게되며
아직 게임이 시작하지 않은 Gameroom이 있다면 Client로 참여하게 됩니다.


## DeathMatch Scene

플레이어는 원하는 팀(Team A 또는 Team B)과 원하는 클래스(Assault, Breacher, Demolition)를 선택한 뒤 **Ready** 버튼을 클릭합니다.
방에 접속한 모든 플레이어가 Ready 상태가 되면 게임이 시작됩니다.

현재 테스트 환경에서는 혼자 접속하더라도 팀 및 클래스 선택 후 **Ready** 버튼을 클릭하면 바로 게임이 시작되도록 설정해 두었습니다.

---

### 조작 방법 

```
W, A, S, D : 상하좌우이동  
마우스 이동 : 조준 및 시야 회전  
마우스 왼쪽 클릭 : 장착한 총기 발사  
G 키 : (Demolition 클래스 전용) 수류탄 투척  
```

---

### 클래스 설명 

* **Assault**

  * 기본 무기: 소총, 권총

* **Breacher**

  * 기본 무기: 샷건, 권총

* **Demolition**

  * 기본 무기: 권총
  * G 키를 이용하여 수류탄을 사용할 수 있음

---

### 승리 조건 및 종료

한 팀의 모든 플레이어가 사망하면 게임이 종료됩니다.
게임 종료 후 **Back to Menu** 버튼을 클릭하여 StartUp Scene으로 돌아갈 수 있습니다.

---

## 5. 프로젝트 구조 

```
/Assets
  /Animations - 캐릭터 및 무기 애니메이션
  /Firebase - Firebase SDK 리소스
  /FOVMapping - 플레이어 시야(FoV) 관련 기능
  /Grenade Pack, Grenade Sound FX - 투척물 에셋 및 사운드
  /Photon - Photon Fusion 네트워크 리소스
  /Prefabs - 게임 오브젝트 프리팹
  /Scenes - Login, Lobby, Gameplay 등의 씬 파일
  /Scripts
    /Gameplay - 게임플레이 로직(투척물, 점수, 팀 등)
    /Login - 로그인/회원 인증
    /Menu - UI 메뉴 흐름
    /Player - 이동, 카메라, 클래스 기능
    /UI - UI 표시 및 컨트롤
    /Utilities - 공용 유틸
    /Weapons - 무기 및 반동 시스템
  /Textures, /Materials, /Models - 그래픽 리소스 전반
```

---

## 6. 기술 스택 

* Unity 2022.3.62f2
* C#
* Photon Fusion
* Firebase Authentication

---

## 7. 팀원

| 이름   | 역할                                      |
| ----   | --------------------------               |
| 박재현  | 팀장, 맵 구현, 총기 반동 시스템            |
| 선현승  | SM, 로그인기능, 버그해결                  |
| 서하진  | 투척물 기능 및 사용자 시야 구현            |
| 이창민  | 줌 및 카메라 개선, 맵 안개 시야 구현,       |
| 한승윤  | 클래스 시스템 및 게임로직 설계              |
---

## 8. 참고자료

1. 데모영상
   - https://youtu.be/1A5cF8DOtZg

2. 프로젝트 소스파일
   - https://drive.google.com/file/d/1OLcdbczZwvLk1xNqVEEQObyVa0kMx2wj/view
