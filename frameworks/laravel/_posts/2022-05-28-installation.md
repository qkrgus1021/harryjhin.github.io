---
title: '[Laravel] 설치하기'
excerpt: '도커를 사용해 라라벨 웹 프레임워크를 빠르게 만나볼 수 있습니다.'
---

## 개요

라라벨은 PHP 언어로 웹 애플리케이션을 만들 때 사용하는 프레임워크 중 하나입니다.

빠른 시작을 위해 도커를 통해 라라벨 앱을 만들 수 있도록 지원합니다.

더 자세한 내용은 [공식 문서](https://laravel.kr/docs/8.x/installation)를 참고하세요.

## 요구사항

1. Docker Desktop이 설치되어 있어야 됩니다.

    아직 설치하지 않은 분들은 다음 명령어를 사용하면 쉽게 설치할 수 있습니다.

    ```powershell
    winget install docker.dockerdesktop
    ```

2. WSL2가 활성화되어 있어야 합니다.
3. `Hyper-V`가 활성화되어 있어야 합니다.
4. Docker Desktop이 WSL2를 백엔드로 사용하도록 설정해야 합니다.
5. Visual Studio Code와 Remote - WSL 익스텐션이 설치되어 있어야 합니다.

## 빠른 시작

1. WSL 프로필 중 하나를 터미널에서 실행합니다.
2. 원하는 디렉토리에서 다음 명령어를 통해 빌드된 새로운 라라벨 프로젝트를 설치합니다.

    ```powershell
    curl -s https://laravel.build/example-app | bash
    ```

    **참고**: 해당 url의 "example-app"은 프로젝트의 이름에 해당되며, 원하는 이름으로 바꾸어 실행해도 됩니다. (예: `curl -s https://laravel.build/my-app | bash`)
    {: .notice--info}

3. 만들어진 프로젝트 디렉토리로 이동합니다.

    ```powershell
    cd example-app
    ```

4. 프로젝트의 루트 디렉토리를 Visual Studio Code로 엽니다.

    ```powershell
    code .
    ```

## 초기 설정

라라벨 프레임워크의 모든 설정 파일은 `config` 디렉토리에 저장됩니다.

기본적으로 설정되어 있기 때문에 추가로 설정할 필요는 거의 없습니다.

주로 살펴볼 부분은 `app.php` 파일입니다. 이 파일은 애플리케이션에 따라 변경할 수 있는 `timezone`, `locale`과 같은 지역과 관련된 옵션 등이 포함되어 있습니다.

**참고**: 관련된 모든 옵션에 대란 설명은 [공식 문서](https://laravel.kr/docs/8.x/configuration)에 있으니 참고하시면 됩니다.
{: .notice-info}
