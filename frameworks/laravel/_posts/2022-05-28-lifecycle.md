---
title: '[Laravel] 생명주기'
excerpt: '라라벨 프레임워크 생명주기에 대해 알면 좀 더 쉽게 애플리케이션을 설계할 수 있습니다.'
---

## 개요

라라벨 웹 애플리케이션은 요청받았을 때 다음 단계를 통해 응답합니다.

1. [`public/index.php`](#1-publicindexphp)
2. [HTTP / Console 커널](#2-http--console-커널)
3. [서비스 프로바이더](#3-서비스-프로바이더)
4. [라우팅](#4-라우팅)
5. [마무리](#마무리)

## 1. `public/index.php`

모든 요청에 대한 시작점에 해당되는 파일입니다. (언어로 따지면 main() 함수에 해당됩니다.)

웹 서버 (Apache/Nginx)의 설정에 따라 모든 요청은 이 파일에 전달됩니다.

많은 코드를 가지고 있지 않고, 프레임워크의 나머지 부분들을 로딩하기 위한 시작점 역할을 하고 있습니다.

이 파일은 컴포저가 생성한 오토로더 정의를 로딩하고, `bootstrap.app.php`에서 라라벨 애플리케이션의 인스턴스를 가져옵니다.

**참고**: 라라벨 프레임워크는 패키지간 의존성을 관리해주는 유틸리티입니다.
{: .notice--info}

즉, 첫 번째로 하는 동작은 **서비스 컨테이너 인스턴스를 생성**하는 것입니다.

**참고**: 서비스 컨테이너는 클래스의 의존성을 관리하고 의존성을 주입하는 도구입니다.
{: .notice--info}

## 2. HTTP / Console 커널

애플리케이션이 시작된 유형에 따라 요청을 HTTP 커널(`app/Http/Kernel.php`)이나 콘솔 커널 둘 중 하나로 보냅니다.

HTTP 커널은 요청이 실행되기 전에 실행될 `bootstrappers` 배열을 정의하는 `Illuminate\Foundation\Http\Kernel` 클래스를 확장합니다.

부트스트래퍼는 오류 처리, 로깅, [환경 감지](https://laravel.kr/docs/8.x/configuration#environment-configuration), 요청이 실제로 처리되기 전에 수행해야 하는 기타 작업을 수행합니다. 일반적으로 이런 클래스는 신경 쓸 필요가 없는 라라벨 내부 설정을 처리합니다.

또한, HTTP 커널은 모든 요청이 애플리케이션에서 처리되기 전에 통과해야 하는 HTTP [미들웨어](https://laravel.kr/docs/8.x/middleware) 목록을 관리합니다. 이러한 미들웨어는 [HTTP 세션](https://laravel.kr/docs/8.x/session) 읽기 및 쓰기, 애플리케이션이 유지 관리 모드에 있는지 확인, [CSRF](https://laravel.kr/docs/8.x/csrf) 토큰 확인 등을 처리합니다.

HTTP 커널의 `handle` 메서드는 `Request`를 수신하고 `Response`를 반환합니다.

즉, 커널은 **전체 애플리케이션을 나타내는 블랙박스**라고 생각하면 됩니다. 이 블랙박스는 **HTTP 요청을 받으면 HTTP 응답을 반환**합니다.

## 3. 서비스 프로바이더

커널 부트스트랩 작업 중 하나는 애플리케이션에 대한 서비스 프로바이더를 로드하는 것입니다.

애플리케이션의 모든 서비스 프로바이더는 `config/app.php` 파일의 `providers` 배열에서 관리됩니다.

라라벨은 `provides` 배열에 있는 서비스 프로바이더들을 각각 인스턴스로 만듭니다.

인스턴스화한 후 모든 프로바이더에서 `register` 메서드가 호출되고, 모든 프로바이더를 등록합니다.

모든 프로바이더가 등록되면 각 프로바이더에서 `boot` 메서드가 호출됩니다. `boot` 메서드가 실행될 때, 동록되고 사용 가능한 모든 컨테이너 바인딩에 의존할 수 있기 때문입니다.

**참고**: 서비스 프로바이더는 라라벨 애플리케이션의 부팅(부트스트래핑)의 가장 핵심이라고 할 수 있습니다. 라라벨의 모든 코어 서비스는 서비스 프로바이더를 통해서 부트스트래핑됩니다.
{: .notice--info}

서비스 프로바이더는 데이터베이스, 대기열, 유효성 검사 및 라우팅 구성 요소와 같은 프레임워크의 다양한 구성 요소를 모두 부트스트랩해야 합니다. 라라벨이 제공하는 모든 주요 기능은 서비스 프로바이더에서 부트스트랩 및 구성합니다. 따라서 서비스 프로바이더는 라라벨 부트스트랩 프로세스에서 가장 중요합니다.

## 4. 라우팅

서비스 프로바이더 중 하나인 `App\Providers\RouteServiceProvider`는 애플리케이션의 `routes` 디렉토리에 포함된 경로 `-route` 파일을 로드합니다.

애플리케이션이 부트스트랩되고 모든 서비스 프로바이더가 등록되면 `Request`가 실행을 위해 라우터로 전달됩니다. 라우터는 `request`를 라우트나 컨트롤러로 디스패치하고 라우트별 미들웨어를 실행합니다.

미들웨어는 애플리케이션에 들어오는 HTTP 요청을 필터링하거나 검사하기 위한 편리한 매커니즘을 제공합니다.

요청이 일치하는 경로에 할당된 모든 미들웨어를 통과하면 경로 또는 컨트롤러 메서드가 실행되고 경로 또는 컨트롤러 메서드에서 반환된 응답은 경로의 미들웨어 체인을 통해 다시 전송됩니다.

## 마무리

경로 또는 컨트롤러 메서드가 응답을 반환하면, 응답은 경로의 미드루에어를 통해 외부로 다시 이동하여 애플리케이션이 나가는 응답을 수정하거나 검사할 수 있는 기회를 제공합니다.

마지막으로 응답이 미들웨어를 통해 다시 이동하면 HTTP 커널의 `handle` 메서드가 응답 개체를 반환하고 `index.php` 파일이 반환된 응답에 대해 `send` 메서드를 호출합니다. `send` 메서드는 응답 내용을 사용자의 웹 브라우저로 보냅니다.