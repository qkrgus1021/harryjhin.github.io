---
title: "Github Pages Guide : Configuration"
permalink: /docs/github/pages/guide/configuration/
excerpt: "_config.yml에 대해 알아보자"
sidebar:
    nav: github_pages_guide
toc: true
---

## Site Settings

### Theme

테마의 Ruby gem 버전을 사용하는 경우 활성화하려면 다음 줄이 필요합니다.

```yaml
theme: minimal-mistakes-jekyll
```

### Skin

제공된 스킨 중 하나를 사용하여 테마의 색 구성표를 쉽게 변경할 수 있습니다.

```yaml
minimal_mistakes_skin: "default" # "air", "aqua", "contrast", "dark", "dirt", "neon", "mint", "plum", "sunrise"
```

#### Air skin: `air`

![air-skin-archive](../../../assets/images/air-skin-archive.png)|![air-skin-post](../../../assets/images/air-skin-post.png)
--|--

#### Aqua skin: `aqua`

![aqua-skin-archive](../../../assets/images/aqua-skin-archive.png)|![aqua-skin-post](../../../assets/images/aqua-skin-post.png)
--|--

#### Contrast skin: `contrast`

![contrast-skin-archive](../../../assets/images/contrast-skin-archive.png)|![contrast-skin-post](../../../assets/images/contrast-skin-post.png)
--|--

#### Dark skin: `dark`

![dark-skin-archive](../../../assets/images/dark-skin-archive.png)|![dark-skin-post](../../../assets/images/dark-skin-post.png)
--|--

#### Dirt skin: `dirt`

![dirt-skin-archive](../../../assets/images/dirt-skin-archive.png)|![dirt-skin-post](../../../assets/images/dirt-skin-post.png)
--|--

#### Mint skin: `mint`

![mint-skin-archive](../../../assets/images/mint-skin-archive.png)|![mint-skin-post](../../../assets/images/mint-skin-post.png)
--|--

#### Neon skin: `neon`

![neon-skin-archive](../../../assets/images/neon-skin-archive.png)|![neon-skin-post](../../../assets/images/neon-skin-post.png)
--|--

#### Neon skin: `plum`

![plum-skin-archive](../../../assets/images/plum-skin-archive.png)|![plum-skin-post](../../../assets/images/plum-skin-post.png)
--|--

#### Sunrise skin: `sunrise`

![sunrise-skin-archive](../../../assets/images/sunrise-skin-archive.png)|![sunrise-skin-post](../../../assets/images/sunrise-skin-post.png)
--|--

### Locale

`site.locale`은 사이트 내의 각 웹 페이지에 대한 기본 언어를 선언하는 데 사용됩니다.

예: `locale: "en-US"`는 사이트의 언어 속성을 미국(`US`)식 영어(`en`)로 설정합니다. 국가 코드는 선택사항이며 따라서 더 짧은 `locale: "en"`도 허용됩니다. 언어 및 국가 코드를 찾으려면 [참조표](https://docs.microsoft.com/en-us/previous-versions/commerce-server/ee825488(v=cs.20)?redirectedfrom=MSDN)를 확인하세요.

```yaml
locale: "en-US" # 한국 설정은 "ko-KR"
```

장소를 올바르게 설정하는 것은 [UI Text] 데이터 파일에서 찾은 현지화된 텍스트를 연결하는 데 중요합니다. 부적절하게 일치하면 UI의 일부가 사라집니다. (제목이나 버튼 레이블 등)

**참고**: 테마는 영어(en, en-US, en-GB)로 현지화된 텍스트와 함께 제공됩니다. `_config.yml`의 로케일을 다른 것으로 변경하면 대부분의 UI 텍스트가 공백이 됩니다. 이를 방지하려면 해당 로케일 키와 번역된 텍스트를 `_data/ui-text.yml`에 추가해야 합니다.
{: .notice--warning}

### Title

사이트 이름입니다. 사이트 masthead 및 `<title>` 태그와 같은 위치에서 테마 전체에 사용됩니다.

```yaml
title: "My Awesome Site"
```

SEO 친화적인 페이지 제목에 사용되는 분리 문자를 사용자 정의할 수도 있습니다.

```yaml
title_separator: "|"
```

**참고**: 긴 사이트 제목은 masthead 레이아웃을 깨는 것으로 알려져 있습니다. 제목에 긴 "태그라인"을 추가하지 마십시오.
{: .notice--warning}

### Subtitle

사이트 masthead의 제목 아래에 표시되는 짧은 태그 라인입니다.

```yaml
subtitle: "version 2.0"
```

### Name

사이트 작성자를 지정하는 데 사용됩니다.

**참고**: 특정 포스트, 페이지 또는 컬렉션 문서에서 사이트 작성자를 다른 작성자로 재정의할 수 있습니다.
{: .notice--warning}

```yaml
name: "홍길동"
```

### Description

사이트를 설명합니다. SEO 개선을 위한 메타 설명에서 주로 사용됩니다.

```yaml
description: "minimal mistakes는 Jekill 테마입니다."
```

### URL

사이트의 기본 호스트 이름 및 프로토콜입니다. Github Pages로 호스팅하는 경우 `url: "https://username.github.io"`이 됩니다. 또는 사용자 지정 도메인 이름이 있는 경우 `url: https://jinhyun.blog`(예시)가 됩니다.

```yaml
url: "https://username.github.io"
```

### Base URL

이 옵션은 링크를 복잡하게 만드는 악의 근원이므로 설정을 안 하는 것이 정신 건강에 이롭다.

Minimal Mistakes 데모 사이트의 경우 Github <https://mmistakes.github.io/minimal-mistakes/>에서 호스팅 됩니다. 이 기본 경로를 올바르게 설정하려면 `url: "https://mmistakes.github.io"` 및 `baseurl: "/minimal-mistakes"`를 사용합니다.

Jekyll 관리자가 의도한 대로 site.url 및 site.baseurl을 올바르게 사용하는 방법에 대한 자세한 내용은 해당 주제에 대한 Parker Moore의 [게시물](https://byparker.com/blog/2014/clearing-up-confusion-around-baseurl/)을 확인하십시오.

```yaml
# baseurl: "/minimal-mistakes"
```

### 

```yaml

```

### 

```yaml

```

### 

```yaml

```

### 

```yaml

```
