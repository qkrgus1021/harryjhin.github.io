---
title: "Jekyll : 로컬에서 테스트"
excerpt: "수정한 내용을 Github Pages의 빌드가 아닌 로컬에서 바로 확인하기"
---

Github Pages 리포지토리(`사용자이름.github.io`) 로 푸시하면 알아서 빌드 후 배포까지 해줍니다.

문제는 여기서 소모되는 시간입니다.

보통 1~2분 정도 걸리는데 테스트 커밋일 경우 내가 생각한 대로 표현이 되었는지 확인하는 데 한 두개면 상관 없지만 여러 개일 경우 너무 오래 걸립니다.

또 다른 문제는 문법적 오류나 잘못된 설정으로 인한 에러가 날 경우 github-pages에만 의존하여 확인하기 너무 어렵습니다.

![Jekyll 로컬 설치가 필요한 이유]({% link /assets/images/jekyll-reason.jpeg %})

그렇기에 로컬 빌드를 통한 로컬호스트 확인이 필요합니다. Jekyll을 설치하여 2~3초면 즉각 테스트할 수 있습니다.

## 필요한 것

- [Jekyll 설치](https://jekyllrb.com/docs/installation/){:target="_blank"}
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
