---
title: "[VS Code] 익스텐션 개발하기"
---

## WSL 개발환경 구축

1. curl 설치

    ```bash
    sudo apt install curl
    ```

2. nvm 설치

    ```bash
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
    ```

3. 터미널을 닫고 열어 nvm 설치를 완료

    ```bash
    command -v nvm
    ```

    `nvm`이 반환되야 합니다.

4. Node.js의 현재 버전과 안정 버전(LTS)를 모두 설치합니다.

    ```bash
    nvm install --lts
    nvm install node
    ```

5. Yeoman, Visual Studio Code Extension Generator 설치

    ```bash
    npm install -g yo generator-code
    ```

6. Generator 실행하기

    ```bash
    yo code
    ```

    아래처럼 옵션 선택하기

    ```md
    ? What type of extension do you want to create? New Extension (JavaScript)
    ? What's the name of your extension? hello-world
    ? What's the identifier of your extension? hello-world
    ? What's the description of your extension?
    ? Enable JavaScript type checking in 'jsconfig.json'? No
    ? Initialize a git repository? Yes
    ```

    `Open with code` 선택

7. `F5` 키를 입력, 만들어진 익스텐션이 적용된 VS Code 새 창이 열립니다. 명령 파레트(Ctrl + Shift + P)를 열어 `Hello World`를 입력하면 우측 하단에 `Hello World from hello-world!` 메시지가 출력됩니다.

본격적인 익스텐션 개발은 `/extension.js`를 수정하고, `> Developer: Reload Window`를 수행하고, `> Hello World`를 수행하면 결과를 확인할 수 있습니다.

## 배포

1. [Azure](https://dev.azure.com/joojinhyun00/?acquisitionId=2bd3b2a8-6471-4339-9876-8bfef1d46fec&acquisition=true)에서 organization을 생성합니다.
2. Person Access Token(PAT)을 발급받습니다.
3. [Create Publish](https://marketplace.visualstudio.com/manage/createpublisher?managePageRedirect=true)를 작성합니다.
4. 익스텐션 디렉토리의 `package.json` 파일 안에 publish를 추가

    ```json
    {
        ...,
        "publisher": "Create Publish에서 만든 publish 이름",
        ...
    }
    ```

5. Visual Studio Code Extension을 설치, 로그인하고 배포

    ```bash
    npm install -g vsce
    vsce login
    vsce publish
    ```
