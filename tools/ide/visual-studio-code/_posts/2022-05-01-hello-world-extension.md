---
title: "[VS Code] hello-world 익스텐션 상세"
---

## 개요

다음과 같이 익스텐션을 생성합니다.

```bash
yo code

# ? What type of extension do you want to create? New Extension (TypeScript)
# ? What's the name of your extension? HelloWorld
### Press <Enter> to choose default for all options below ###

# ? What's the identifier of your extension? helloworld
# ? What's the description of your extension? LEAVE BLANK
# ? Initialize a git repository? Yes
# ? Bundle the source code with webpack? No
# ? Which package manager to use? npm

# ? Do you want to open the new folder with Visual Studio Code? Open with `code`
```

이렇게 만들어진 `Hello World` 익스텐션은 3가지 작업을 수행합니다.

- Activation Event(활성화 이벤트) 등록: 사용자가 명령을 실행할 때 익스텐션이 활성화됩니다.
- Contribution Point(명령 지점): 명령 팔레트에서 명령을 사용할 수 있도록 명령 ID에 바인딩합니다.
- VS Code API를 사용하여 등록된 명령 ID에 함수를 바인딩합니다.

익스텐션 개발을 하려면 세 가지 개념을 알아야 합니다.

- 활성화 이벤트: 익스텐션이 활성화되는 이벤트입니다.
- 명령 지점: VS Code를 확장하기 위해 `package.json` 익스텐션 매니페스트에서 만드는 정적 선언입니다.
- VS Code API: 익스텐션 코드에서 호출할 수 있는 JavaScript API 세트입니다.

일반적으로 명령 지점과 VS Code API를 조합해 익스텐션을 만듭니다.

## 익스텐션 파일 구조

```markdown
.
├── .vscode
│   ├── launch.json     // 익스텐션 프로그램 실행 및 디버깅을 위한 구성
│   └── tasks.json      // TypeScript를 컴파일하는 빌드 작업에 대한 구성
├── .gitignore          // 빌드 출력 및 node_modules 무시
├── README.md           // 익스텐션 기능을 설명하는 읽기 쉬운 설명
├── src
│   └── extension.ts    // 익스텐션 소스 코드
├── package.json        // 익스텐션 매니페스트
├── tsconfig.json       // TypeScript 구성
```

우리는 익스텐션의 핵심인 `package.json`에 집중합니다.

### 익스텐션 매니페스트

VS Code 익스텐션에는 익스텐션 매니페스트로 `package.json` 파일이 있어야 합니다. `package.json`에는 스크립트 및 devDependencies와 같은 Node.js 필드와 퍼블리셔, 활성화 이벤트, 명령과 같은 VS Code 특정 필드가 포함되어 있습니다.

이 중 핵심은 다음과 같습니다.

- `name`, `publisher`: VS Code는 익스텐션의 고유 ID로 `publisher.name`을 사용합니다.
- `main`: 익스텐션 진입점.
- `activationEvents`: 활성화 이벤트
- `contributes`: 기여점
- `engins.vscode`: 이 익스텐션이 의존하는 VS Code API의 최소 버전을 지정합니다.

```typescript
{
  "name": "helloworld-sample",
  "displayName": "helloworld-sample",
  "description": "HelloWorld example for VS Code",
  "version": "0.0.1",
  "publisher": "vscode-samples",
  "repository": "https://github.com/microsoft/vscode-extension-samples/helloworld-sample",
  "engines": {
    "vscode": "^1.51.0"
  },
  "categories": ["Other"],
  "activationEvents": ["onCommand:helloworld.helloWorld"],
  "main": "./out/extension.js",
  "contributes": {
    "commands": [
      {
        "command": "helloworld.helloWorld",
        "title": "Hello World"
      }
    ]
  },
  "scripts": {
    "vscode:prepublish": "npm run compile",
    "compile": "tsc -p ./",
    "watch": "tsc -watch -p ./"
  },
  "devDependencies": {
    "@types/node": "^8.10.25",
    "@types/vscode": "^1.51.0",
    "tslint": "^5.16.0",
    "typescript": "^3.4.5"
  }
}
```

## 익스텐션 엔트리 파일(extension.js)

익스텐션 엔트리 파일은 활성화(activate), 비활성화(deactivate)라는 두 가지 기능을 내보냅니다.

- 활성화는 등록된 활성화 이벤트가 발생할 때 실행됩니다.
- 비활성화는 익스텐션이 비활성되기 전에 정리할 기회를 제공합니다. 이 옵션은 선택적입니다.

VS Code 익스텐션 API는 [@types/vscode](https://www.npmjs.com/package/@types/vscode) 타입 정의에 선언되어 있습니다. vscode 타입 정의의 버전은 `package.json`의 `engines.vscode` 필드 값으로 제어합니다. vscode 타입은 코드에서 IntelliSense, 정의로 이동 및 기타 TypeScript 언어 기능을 제공합니다.

```javascript
// The module 'vscode' contains the VS Code extensibility API
// Import the module and reference it with the alias vscode in your code below
import * as vscode from 'vscode';

// this method is called when your extension is activated
// your extension is activated the very first time the command is executed
export function activate(context: vscode.ExtensionContext) {
  // Use the console to output diagnostic information (console.log) and errors (console.error)
  // This line of code will only be executed once when your extension is activated
  console.log('Congratulations, your extension "helloworld-sample" is now active!');

  // The command has been defined in the package.json file
  // Now provide the implementation of the command with registerCommand
  // The commandId parameter must match the command field in package.json
  let disposable = vscode.commands.registerCommand('helloworld.helloWorld', () => {
    // The code you place here will be executed every time your command is executed

    // Display a message box to the user
    vscode.window.showInformationMessage('Hello World!');
  });

  context.subscriptions.push(disposable);
}

// this method is called when your extension is deactivated
export function deactivate() {}
```

## 익스텐션 기능

### 공통 기능

공통 기능은 모든 확장에서 사용할 수 있는 핵심 기능입니다.

대표적인 기능은 다음과 같습니다.

- 명령, 구성, 키 바인딩, 상황에 맞는 메뉴 항목 등록
- 작업 공간 또는 글로벌 데이터를 저장
- 알림 메시지를 표시
- 빠른 선택을 사용해 사용자 입력 수집
- 사용자가 파일이나 폴더를 선택할 수 있도록 시스템 파일 선택기 열기
- Progress API를 사용해 장기 실행 작업을 표시

#### 커맨드(command)

명령 팔레트를 열어 명령을 실행하고 사용자 지정 키 바인딩을 명령에 바인딩하고 마우스 오른쪽 버튼을 클릭하여 상황에 맞는 메뉴에서 명령을 호출합니다.

## UX 가이드라인

