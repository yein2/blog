---
title: Unity Project Set up
---

# Unity Project Set up
## 🌞│**Unity 설치**
1. Unity Hub 설치

   - [Unity Hub 설치](https://unity.com/kr/download) 접속
   
        <img src="../images/UnityHubDownload.png">
        

   - 원하는 경로 지정 후 설치

        <img src="../images/UnityInstall_1.png">

        <img src="../images/UnityInstall_2.png">

2. Unity Download Archive

   - [Unity Version Archive](https://unity3d.com/kr/get-unity/download/archive) 접속

        <img src="../images/UnityVersionDownload.png">

   - 원하는 모듈 선택 후 설치

        <img src="../images/UnityModuleInstalll.png">

## ☔│**Unity 모듈 추가**
- 이미 설치된 버전에서 모듈을 추가 하고 싶을 경우
- 모듈을 추가할 버전 열기

    <img src="../images/UnityAddModule_1.png">

- 모듈 추가 누르기

    <img src="../images/UnityAddModule_2.png">

- 원하는 모듈 선택 후 설치

    <img src="../images/UnityAddModule_3.png">
## ⛅│**Unity 라이선스 관리**
- Unity Hub 로그인 하기

    <img src="../images/Login.png">

- 라이선스 관리로 이동
- 새 라이선스 활성화 누르기

    <img src="../images/LicenseManage.png">

- 홈페이지에서 시리얼 키 확인하기

    <img src="../images/CheckCerealKey.png">

- 시리얼 키 등록 후 라이선스 활성화

    <img src="../images/RegisterLicense.png">


## 🍂│**Unity Platform**
- 작업을 시작하기 전 알맞은 플랫폼을 적용시켜야 함
- `File` - `Build Settings...`를 눌러 Build Settings 창 띄우기
- 알맞은 `Platform`을 선택하고 `Switch Platform` 누르기

    <img src="../images/BuildSetting.png">


## ⛄│**Unity Project Folder**
- 프로젝트를 효율적으로 관리하기 위해 작업을 들어가기 전 어떤 폴더 구조를 사용할 지 작업자끼리 논의가 필요함
- 폴더 구조에 대한 정답은 정해져 있지 않으나 작업자끼리 헷갈리지 않게 폴더 규칙을 정해야 함
### 🔸 예시 (2022.7.5 기준 폴더 구조)

<img src="../images/UnityFolder.png">

### 🔸 모범사례 예시
- [출처](https://sam-16930.medium.com/unity-project-structure-a694792cefed)
- Project 구조

|  폴더명  |  필수  |  설명  |
| :-------- | :----------: | :----------: |
| .vscode | X | Visual Studio Code 설정 파일 |
| Asset | O | Unity 프로젝트 리소스가 들어갈 기준 파일 |
| Library | X | Unity에서 포함될 Library 폴더 |
| Logs | X | Unity에서 기록되는 Log 폴더 |
| obj | X | 연결되지 않은 컴파일된 바이너리 파일의 중간 파일 저장소 |
| Packages | O | Unity Projet에 포함될 Packages 폴더
| ProjectSetting | X | Unity Project Setting의 설정 파일이 포함된 폴더 |

- Asset 구조
```
Assets
├── 3rdParty
│   ├── [VendorName]
│   ├── readme.txt (Manually created. Source URL & changelog)
│   └── [PackageName]
├── Art
│   ├── Animators
│   ├── AnimationClips
│   ├── Fonts
│   ├── Materials
│   ├── Models
│   ├── Shaders
│   ├── Sprites
│   └── Textures
├── Audio
│   ├── AudioClips
│   └── AudioMixers
├── Documentation
├── PhysicMaterials
├── Prefabs
│   └── RMC
│       └── [MyProject]
│           └── MyHeroPrefab (using MyHero.cs)
├── Presets
├── Resources
├── Scenes
├── ScriptableObjects
│   └── RMC
│       └── [MyProject]
│           └── MyHeroSettings (using MyHeroSettings.cs)
└── Scripts
    ├── Editor
    │   └── RMC
    │       └── [MyProject]
    │           └── MyHeroEditor.cs (namespace RMC.MyProject)
    ├── Runtime
    │   └── RMC
    │       └── [MyProject]
    │           └── MyHero.cs (namespace RMC.MyProject)
    └── Tests
        └── Editor
            └── RMC
                └── [MyProject]
                    └── MyHeroTest.cs (namespace RMC.MyProject)
```
- Asset 간소화
```
Assets
├─ Animation
│        ├─ Clips
│        └─ Controllers
├─ Audio
│        ├─ Enemy
│        ├─ FX
│        ├─ Music
│        └─ Player
├─ Fonts
├─ Materials
├─ Physics Materials
│        ├─ Characters
│        ├─ Environment
│        ├─ FX
│        ├─ Props
│        └─ UI
├─ Scenes
├─ Scripts
├─ Sprites
│        ├─ Characters
│        ├─ Environment
│        ├─ FX
│        ├─ Props
│        └─ UI
└─ Prefabs
```

## 🌈│**Plastic SCM**

### 🔹 Plastic SCM 이란 ?

{{< youtube u1imEon8Gko >}}

### 🔹 프로젝트 적용 방법
- `Window` - `Plastic SCM` 누르기
- 새로운 워크스페이스 만들기

<img src="../images/PlasticSCM_1.png">

<img src="../images/PlasticSCM_2.png">

- 사용 예시

<img src="../images/PlasticSCM_Example.png">