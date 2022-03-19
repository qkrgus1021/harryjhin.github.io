---
permalink: /windows/powertoys/
title: "PowerToys"
excerpt: "Microsoft PowerToys는 고급 사용자가 생산성을 높이기 위해 Windows 환경을 조정하고 간소화하는 데 사용할 수 있는 유틸리티 세트입니다."
header:
  actions:
    - label: "<i class='fab fa-fw fa-github'></i> 공식 리포지토리 바로가기"
      url: "https://github.com/microsoft/PowerToys"
taxonomy: powertoys
---

## 프로세서 지원

- x64: 지원
- ARM: 개발 중

## 현재 PowerToys 유틸리티

현재 사용할 수 있는 유틸리티는 다음과 같습니다.

|<center>유틸리티</center>                                                             |<center>설명</center>                                                                  |
|--------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------|
|[Always on Top]({{ site.url }}/windows/powertoys/always-on-top/)                      |어떤 창을 모든 창 위에 위치하도록 하는 기능                                            |
|[PowerToys Awake]({{ site.url }}/windows/powertoys/awake/)                            |시스템의 전원 설정을 변경할 필요 없이 내가 원하는 대로 절전 시간을 변경할 수 있는 기능 |
|[Color Picker]({{ site.url }}/windows/powertoys/color-picker/)                        |마우스 커서 위치에 있는 픽셀의 색을 색상 코드로 알 수 있는 기능                        |
|[FancyZones]({{ site.url }}/windows/powertoys/fancy-zones/)                           |창 레이아웃을 내가 원하는 레이아웃으로 커스터마이징 할 수 있는 기능                    |
|[File Explorer Add-ons]({{ site.url }}/windows/powertoys/file-explorer-add-ons/)      |파일 탐색기의 미리보기 창을 통해 볼 수 있는 파일의 종류를 확장하는 기능                |
|[Image Resizer]({{ site.url }}/windows/powertoys/image-resizer/)                      |이미지의 사이즈를 내가 원하는 크기로 변경할 수 있는 기능                               |
|[Keyboard Manager]({{ site.url }}/windows/powertoys/keyboard-manager/)                |키를 매핑하여 나만의 고유 단축키를 만들 수 있는 기능                                   |
|[Mouse utilities]({{ site.url }}/windows/powertoys/mouse-utilities/)                  |마우스 커서의 위치를 보다 명확하게 인지할 수 있게 해주는 기능                          |
|[PowerRename]({{ site.url }}/windows/powertoys/power-rename/)                         |다수의 파일 이름을 원하는대로 한 번에 변경할 수 있는 기능                              |
|[PowerToys Run]({{ site.url }}/windows/powertoys/run/)                                |앱을 검색하여 실행하거나 웹을 검색할 수 있는 기능                                      |
|[Shortcut Guide]({{ site.url }}/windows/powertoys/shortcut-guide/)                    |윈도우 바탕화면에서 사용할 수 있는 단축키를 그래픽으로 보여주는 기능                   |
|[Video Conference Mute]({{ site.url }}/windows/powertoys/video-conference-mute/)      |무엇을 하고 있던지 카메라와 마이크를 시스템적으로 빠르게 음소거할 수 있는 기능         |

## 설치하는 방법

PowerToys를 설치하는 방법은 3가지가 있습니다.

- [앱 설치 관리자(`winget` 명령어)](#winget)
- [마이크로소프트 스토어](#microsoft-store)
- [깃허브 릴리즈](#github-release)

본인이 잘 아는 도구를 통해서 아래 절차에 따라 진행하시면 됩니다.

### Winget

1. PowerShell을 관리자 권한으로 실행
2. 다음 명령어를 입력

   ```ps
   winget install Microsoft.PowerToys
   ```

### Microsoft Store

1. Microsoft Store 실행
2. 'PowerToys' 검색
3. 'Microsoft Powertoys' 설치

### Github Release

1. <https://github.com/microsoft/PowerToys/releases/> 클릭
2. `PowerToysSetup-0.nn.n-x64.exe` 다운로드 및 실행

## 관련 포스트

---
