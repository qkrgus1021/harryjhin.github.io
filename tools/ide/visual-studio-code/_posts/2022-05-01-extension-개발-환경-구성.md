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

## 퍼블리싱

필요한 것:

- vsce CL 설치
- Personal Access Token 생성
- 퍼블리셔 생성
- 게시

### vsce

vsce(Visual Studio Code Extension)은 익스텐션을 패키징, 퍼블리싱, 매니징하기 위한 CL 도구입니다.

또, 메타데이터를 검색하거나 익스텐션 퍼블리싱을 취소할 수 있습니다.

#### 설치

```bash
npm install -g vsce
```

#### 사용법

```bash
cd <내 익스텐션 디렉토리>
vsce package
vsce publish
```

### Personal Access Token 받기

1. DevOps에서 [새로운 조직 만들기](https://aex.dev.azure.com/go/signup?account=true&campaign=o~msft~vsts~orghome)
2. 조직 홈 페이지(예: `https://dev.azure.com/vscode`)에서 프로필 이미지 옆에 있는 사용자 설정 드롭다운 메뉴를 열고 Personal Access Token을 선택
3. `New Token`을 선택하여 새로운 Personal Access Token을 만들고 다음 세부 정보를 설정합니다.
    - Name: 이름 짓기
    - Organization: All accessible organization 선택
    - Expiration: 선택적으로 만료 날짜를 연장
    - Marketplace: Manage를 체크합니다.
4. Create를 선택하면 새로 만든 Personal Access Token이 표시됩니다. 미리 복사해둡니다.

### 퍼블리셔 생성

퍼블리셔(publisher)는 Visual Studio Code Marketplace에 익스텐션을 퍼블리싱 할 수 있는 ID 입니다. 모든 익스텐션은 `package.json` 파일에 `publisher` 이름을 포함해야 합니다.

1. 마켓플레이스에서 퍼블리셔를 [생성](https://marketplace.visualstudio.com/manage)합니다. Personal Access Token을 생성한 계정으로 로그인합니다.
2. vsce를 사용해 퍼블리셔의 Personal Access Token을 테스트하는 동시에 나중에 사용할 수 있도록 저장합니다.

    ```bash
    vsce login <퍼블리셔 이름>
    ```

### 게시

게시는 다음 명령어로 합니다.

```bash
vsce publish
```

또는 마켓플레이스에 직접 수동으로 게시할 수 있습니다.

## 익스텐션 버전 자동 증가

증가할 [Semantic Version](https://semver.org/) 호환 숫자(major, minor, patch)를 지정하여 게시할 때 익스텐션의 숫자를 자동으로 증가시킬 수 있습니다.

예를 들어, 익스텐션 버전을 1.0.0에서 1.1.0으로 업데이트할 때는 `minor`를 사용합니다.

```bash
vsce publish minor
```

이렇게 하면 게시전 `package.json`의 `version` 속성이 변경됩니다.
