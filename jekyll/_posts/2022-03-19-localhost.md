---
title: "[지킬] 로컬호스트"
excerpt: "로컬에 지킬을 설치하고 프로젝트를 빌드해 바로 브라우저를 통해 확인할 수 있습니다."
---

## 개요

**참고**: 이 블로그는 [**Github Pages**](https://pages.github.com/)[^1]를 통해 서비스되고 있습니다.
{: .notice--info}

Github 리포지토리에 변경 사항을 푸시하면 github-pages가 빌드하고 배포까지 하는 데 보통 1~2분 정도 소요됩니다. 설정 값이 잘못되었거나 문법에 오류가 있을 경우 빌드에 실패하고 이전 배포 버전으로 유지됩니다.

만약 본인이 테스트 목적으로 여러 변경 시도가 필요하다면 배포까지 분 단위로 걸리는 과정이 부담스러워집니다. 변경한 것이 내가 원한 결과인지 확인하는 시간도 오래 걸립니다.

따라서, Github 리포지토리의 안정적인 버전 유지와 미리 테스트하고 푸시할 수 있는 환경이 바람직하다고 볼 수 있습니다.

![Jekyll 로컬 설치가 필요한 이유]({% link /assets/images/jekyll-reason.jpeg %})

{% include figure image_path="/assets/images/jekyll-reason.jpeg" alt="" caption="~~대참사~~" %}

~~대참사~~

## 필요한 것

- [Jekyll 설치](https://jekyllrb.com/docs/installation/)
- Jekyll로 만든 사이트 프로젝트 리포지토리

Bundler를 사용하여 Jekyll을 설치하고 실행할 것을 권장합니다. Bundler는 Ruby gem의 종속성을 관리하고 Jekyll 빌드 오류를 줄이며 환경 관련 버그를 방지합니다.

### WSL(Ubuntu)에서 설치

필자는 개발환경을 WSL에서 관리합니다. 따라서 Ubuntu에서 어떻게 설치하는지 설명하겠습니다.

{% highlight bash %}

sudo apt-get install ruby-full build-essential zlib1g-dev

{% endhighlight %}

루트 사용자로 설치하지 마세요. 사용자 계정에 gem 디렉토리를 설정하면 됩니다. 다음 명령은 `~./bashrc` 파일에 환경 변수를 추가하여 gem 설치 경로를 구성합니다.

{% highlight bash %}

echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc

{% endhighlight %}

마지막으로 Jekyll 및 Bundler를 설치합니다.

{% highlight bash %}

gem install jekyll bundler

{% endhighlight %}

## 로컬에서 사이트 빌드

1. 터미널 열기
2. 사이트 리포지토리 디렉토리로 이동
3. `bundle install` 명령 실행
4. `bundle exec jekyll serve` 명령 실행
5. <http://127.0.0.1:4000> 접속

## Github Pages gem 업데이트

Jekyll은 자주 업데이트되는 인기만점 오픈 소스 프로젝트입니다. 로컬의 `github-pages` gem이 Github Pages 서버의 gem보다 하위 버전일 수 있습니다. 이로 인해 로컬로 빌드 했을 때 Github에 게시될 때와 다르게 보일 수 있습니다. 이를 방지하기 위해 정기적으로 `github-pages` gem을 업데이트해야 합니다.

1. 터미널 열기
2. `bundle update github-pages`

앞으로 Jekyll 테스트 하는데 시간낭비하는 일 없기를...

[^1]: 기존 블로그 서비스(티스토리, 네이버 블로그 등)들과는 다르게 Github 리포지토리에서 직접 호스팅됩니다. 푸시하면 수정된 변경 사항이 적용됩니다. 상당히 개발자 감성이 물씬 나는 서비스여서 개발자 감성을 충족시키나 그만큼 많은 공부가 필요한 서비스입니다. 여유가 많은 사람만 사용하는 것을 권장합니다.
