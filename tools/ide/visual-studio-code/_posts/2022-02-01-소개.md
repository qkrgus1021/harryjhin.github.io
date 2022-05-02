---
title: Visual Studio Code
excerpt: 비주얼 스튜디오 코드 IDE 설정에 대해 설명합니다.
---

## 실행 및 디버그

실행 및 디버그는 `Ctrl` + `Shift` + `D` 단축키를 통해 사이드바에서 확인할 수 있습니다.

여기서 실행 및 디버그의 옵션을 사전에 설정할 수 있습니다.

사전 설정하는 방법은 '실행 및 디버그를 사용자 지정하려면 launch.json 파일 만들기를 수행합니다.' 문구의 launch.json 파일 만들기를 클릭합니다. 그러면 프로젝트 루트 디렉토리에 `.vscode` 폴더와 안에 `launch.json` 파일이 생성됩니다.

**참고**: `.vscode` 폴더는 Visual Studio Code에서만 사용되는 프로젝트 구성 폴더입니다. 따라서 Github와 같은 원격 리포지토리에 푸시할 때 `.gitignore` 파일에 추가하여 무시하는 것이 좋습니다.
{: .notice--info}

### Java

#### assert 활성화

기본적으로 assert 기능이 비활성화되어 있습니다. 따라서 활성화하기 위해 사전 작업이 필요합니다.

1. `launch.json` 생성
2. `"vmArgs": "-ea` 추가

만약 `AssertionTest.java` 파일에 `assert`를 활성화하고자 한다면 다음과 같이 작성하면 됩니다.

```json
{
    "version": "0.2.0",
    "configurations": [
        ...,
        {
            "type": "java",
            "name": "Launch AssertionTest",
            "request": "launch",
            "mainClass": "Assertions.AssertionTest",
            "projectName": "Practice_a248668",
            "vmArgs": "-ea"
        },                                  
        ...
    ]
}
```

`AssertionTest.java` 파일에 `assert`를 사용하고 싶다면 `launch.json`의 `configurations` 중 `mainClass`의 속성이 원하는 클래스인지 확인하고 해당 위치에 `vmArgs` 속성을 추가하고 `-ea` 값을 지정합니다.
