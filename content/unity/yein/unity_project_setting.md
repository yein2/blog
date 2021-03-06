---
title: Unity Project Set up
---

# Unity Project Set up
## πβ**Unity μ€μΉ**
1. Unity Hub μ€μΉ

   - [Unity Hub μ€μΉ](https://unity.com/kr/download) μ μ
   
        <img src="../images/UnityHubDownload.png">
        

   - μνλ κ²½λ‘ μ§μ  ν μ€μΉ

        <img src="../images/UnityInstall_1.png">

        <img src="../images/UnityInstall_2.png">

2. Unity Download Archive

   - [Unity Version Archive](https://unity3d.com/kr/get-unity/download/archive) μ μ

        <img src="../images/UnityVersionDownload.png">

   - μνλ λͺ¨λ μ ν ν μ€μΉ

        <img src="../images/UnityModuleInstalll.png">

## ββ**Unity λͺ¨λ μΆκ°**
- μ΄λ―Έ μ€μΉλ λ²μ μμ λͺ¨λμ μΆκ° νκ³  μΆμ κ²½μ°
- λͺ¨λμ μΆκ°ν  λ²μ  μ΄κΈ°

    <img src="../images/UnityAddModule_1.png">

- λͺ¨λ μΆκ° λλ₯΄κΈ°

    <img src="../images/UnityAddModule_2.png">

- μνλ λͺ¨λ μ ν ν μ€μΉ

    <img src="../images/UnityAddModule_3.png">
## ββ**Unity λΌμ΄μ μ€ κ΄λ¦¬**
- Unity Hub λ‘κ·ΈμΈ νκΈ°

    <img src="../images/Login.png">

- λΌμ΄μ μ€ κ΄λ¦¬λ‘ μ΄λ
- μ λΌμ΄μ μ€ νμ±ν λλ₯΄κΈ°

    <img src="../images/LicenseManage.png">

- ννμ΄μ§μμ μλ¦¬μΌ ν€ νμΈνκΈ°

    <img src="../images/CheckCerealKey.png">

- μλ¦¬μΌ ν€ λ±λ‘ ν λΌμ΄μ μ€ νμ±ν

    <img src="../images/RegisterLicense.png">


## πβ**Unity Platform**
- μμμ μμνκΈ° μ  μλ§μ νλ«νΌμ μ μ©μμΌμΌ ν¨
- `File` - `Build Settings...`λ₯Ό λλ¬ Build Settings μ°½ λμ°κΈ°
- μλ§μ `Platform`μ μ ννκ³  `Switch Platform` λλ₯΄κΈ°

    <img src="../images/BuildSetting.png">


## ββ**Unity Project Folder**
- νλ‘μ νΈλ₯Ό ν¨μ¨μ μΌλ‘ κ΄λ¦¬νκΈ° μν΄ μμμ λ€μ΄κ°κΈ° μ  μ΄λ€ ν΄λ κ΅¬μ‘°λ₯Ό μ¬μ©ν  μ§ μμμλΌλ¦¬ λΌμκ° νμν¨
- ν΄λ κ΅¬μ‘°μ λν μ λ΅μ μ ν΄μ Έ μμ§ μμΌλ μμμλΌλ¦¬ ν·κ°λ¦¬μ§ μκ² ν΄λ κ·μΉμ μ ν΄μΌ ν¨
### πΈ μμ (2022.7.5 κΈ°μ€ ν΄λ κ΅¬μ‘°)

<img src="../images/UnityFolder.png">

### πΈ λͺ¨λ²μ¬λ‘ μμ
- [μΆμ²](https://sam-16930.medium.com/unity-project-structure-a694792cefed)
- Project κ΅¬μ‘°

|  ν΄λλͺ  |  νμ  |  μ€λͺ  |
| :-------- | :----------: | :----------: |
| .vscode | X | Visual Studio Code μ€μ  νμΌ |
| Asset | O | Unity νλ‘μ νΈ λ¦¬μμ€κ° λ€μ΄κ° κΈ°μ€ νμΌ |
| Library | X | Unityμμ ν¬ν¨λ  Library ν΄λ |
| Logs | X | Unityμμ κΈ°λ‘λλ Log ν΄λ |
| obj | X | μ°κ²°λμ§ μμ μ»΄νμΌλ λ°μ΄λλ¦¬ νμΌμ μ€κ° νμΌ μ μ₯μ |
| Packages | O | Unity Projetμ ν¬ν¨λ  Packages ν΄λ
| ProjectSetting | X | Unity Project Settingμ μ€μ  νμΌμ΄ ν¬ν¨λ ν΄λ |

- Asset κ΅¬μ‘°
```
Assets
βββ 3rdParty
β   βββ [VendorName]
β   βββ readme.txt (Manually created. Source URL & changelog)
β   βββ [PackageName]
βββ Art
β   βββ Animators
β   βββ AnimationClips
β   βββ Fonts
β   βββ Materials
β   βββ Models
β   βββ Shaders
β   βββ Sprites
β   βββ Textures
βββ Audio
β   βββ AudioClips
β   βββ AudioMixers
βββ Documentation
βββ PhysicMaterials
βββ Prefabs
β   βββ RMC
β       βββ [MyProject]
β           βββ MyHeroPrefab (using MyHero.cs)
βββ Presets
βββ Resources
βββ Scenes
βββ ScriptableObjects
β   βββ RMC
β       βββ [MyProject]
β           βββ MyHeroSettings (using MyHeroSettings.cs)
βββ Scripts
    βββ Editor
    β   βββ RMC
    β       βββ [MyProject]
    β           βββ MyHeroEditor.cs (namespace RMC.MyProject)
    βββ Runtime
    β   βββ RMC
    β       βββ [MyProject]
    β           βββ MyHero.cs (namespace RMC.MyProject)
    βββ Tests
        βββ Editor
            βββ RMC
                βββ [MyProject]
                    βββ MyHeroTest.cs (namespace RMC.MyProject)
```
- Asset κ°μν
```
Assets
ββ Animation
β        ββ Clips
β        ββ Controllers
ββ Audio
β        ββ Enemy
β        ββ FX
β        ββ Music
β        ββ Player
ββ Fonts
ββ Materials
ββ Physics Materials
β        ββ Characters
β        ββ Environment
β        ββ FX
β        ββ Props
β        ββ UI
ββ Scenes
ββ Scripts
ββ Sprites
β        ββ Characters
β        ββ Environment
β        ββ FX
β        ββ Props
β        ββ UI
ββ Prefabs
```

## πβ**Plastic SCM**

### πΉ Plastic SCM μ΄λ ?

{{< youtube u1imEon8Gko >}}

### πΉ νλ‘μ νΈ μ μ© λ°©λ²
- `Window` - `Plastic SCM` λλ₯΄κΈ°
- μλ‘μ΄ μν¬μ€νμ΄μ€ λ§λ€κΈ°

<img src="../images/PlasticSCM_1.png">

<img src="../images/PlasticSCM_2.png">

- μ¬μ© μμ

<img src="../images/PlasticSCM_Example.png">