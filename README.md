# Github Pages with Minimal Mistakes Theme

Minimal Mistakes 테마를 시작하는 가장 빠른 방법을 보려면 위의 [이 템플릿 사용](https://github.com/mmistakes/mm-github-pages-starter/generate) 버튼을 클릭하세요.

다음과 같은 사이트를 제공하는 기본 구성이 포함되어 있습니다.

- 샘플 포스트가 있는 `_posts` 폴더
- 카테고리 페이지로 이동 가능한 상단 네비게이션바 `navigation.yml` 파일
- 소셜(트위터, 페이스북 등) 링크가 있는 작성자 사이드바
- 소셜 링크가 있는 footer 링크
- 페이지를 매긴 홈페이지
- 연도, 카테고리, 태그 별로 그룹화된 게시물의 아카이브 페이지
- 블로그에 대한 소개를 하는 `about` 페이지
- 에러가 났을 때 사용하는 `404` 페이지
- 사이트 전체 검색

샘플을 자신의 것으로 교체하고 필요에 따라 [구성](https://mmistakes.github.io/minimal-mistakes/docs/configuration/)합니다.

---

## Github Pages

[**Github Pages**](https://pages.github.com/)는 Github 저장소에서 직접 호스팅됩니다. 즉, 저장소에 커멧하면 변경 사항이 적용됩니다. 적용하는데 보통 1분 정도 소요됩니다.

## 지킬(Jekyll)

Jekyll은 정적 사이트 생성기입니다. 별다른 학습이 필요 없는 마크업(Markdown) 언어로 작성된 텍스트 파일을 Jekyll이 레이아웃을 사용해 정적 웹사이트를 생성합니다.

### 디렉토리 구조

```
.
├── _data
│   └── navigation.yml
├── _drafts # 초안
│   └── 초안제목.md
├── _includes
│   ├── footer.html
│   └── header.html
├── _layouts # 포스트 템플릿
│   ├── default.html
│   └── post.html
├── _posts # 포스트
│   ├── YYYY-MM-DD-title.md
│   └── 2009-04-26-my-first-post.md
├── _sass # 사이트 스타일시트
│   ├── _base.scss
│   └── _layout.scss
├── _site # jekyll serve 결과물
├── assets
│   ├── css
│   └── images
├── _config.yml
├── .gitignore
├── CNAME # 커스텀 DNS
└── index.md # `index.html`도 가능
```

각 파일과 디렉토리가 하는 일의 개요는 다음과 같습니다:

| 파일 / 디렉토리 | 설명                                                                                                                                                                                                                                                                      |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `_data`         | 사이트에 사용할 데이터를 적절한 포맷으로 저장한 디렉토리입니다. 이 디렉토리에 있는 파일의 확장자가 `yml`, `json`, `csv`, `tsv`인 경우 모든 데이터를 자동으로 읽어들여 `site.data`로 사용할 수 있습니다. 또한 사이트의 내비게이션 및 사이드바에 대한 yaml 파일도 있습니다. |
| `_drafts`       | 포스트 초안을 저장한 디렉토리입니다. 초안이란 아직 게시하지 않은 포스트를 의미합니다. 저장 형식은 `title.md`입니다.                                                                                                                                                       |
| `_includes`     | 재사용하기 위한 파일을 담는 디렉토리입니다. 포스트나 레이아웃에 삽입합니다. 삽입 방식은 `{% raw %}{% include file.ext %}{% endraw %}`와 같이 Liquid 태그를 사용합니다.                                                                                                    |
| `_layouts`      | 포스트의 템플릿이 저장되어 있는 디렉토리입니다. Yaml Front Matter에서 레이아웃을 선택합니다.                                                                                                                                                                              |
| `_pages`        | 페이지를 저장한 디렉토리입니다. 페이지는 포스트의 카테고리(경로)의 역할을 하거나 컬렉션을 보여주는 역할도 겸합니다. 저장 형식은 `title.md`입니다.                                                                                                                         |
| `_posts`        | 포스트를 저장한 디렉토리입니다. 포스트는 블로그에서 작성되는 글을 의미하며 콘텐츠입니다. 저장 형식은 'YYYY-MM-DD-title.md`입니다.                                                                                                                                         |
| `_sass`         | `main.scss`에 임포트할 scss 파일을 저장한 디렉토리입니다. 하나의 스타일시트 파일 `main.css`로 가공되어 사이트에서 사용할 스타일을 정의합니다.                                                                                                                             |
| `_site`         | 로컬에서 `jekyll serve` 명령어를 사용하여 빌드할 경우 생성되는 디렉토리입니다. 변환 작업이 끝난 파일을 저장하며 `.gitignore`에 추가하여 제외해도 좋습니다.                                                                                                                |
| `assets`        | 사이트에서 사용할 이미지, css 파일 등이 저장되어 있는 디렉토리입니다. 용도와 목적별로 다양하게 구분하여 저장됩니다.                                                                                                                                                       |
| `_config.yml`   | 환경 설정 정보를 담은 파일입니다.                                                                                                                                                                                                                                         |
| `.gitignore`    | 원격 리포지토리에 커밋 대상에서 제외한 파일과 디렉토리 정보가 있는 파일입니다. 빌드 후 생기는 `_site`가 대표적인 대상입니다.                                                                                                                                              |
| `CNAME`         | Github Pages 옵션에서 자신만의 DNS를 연결하면 생성되는 파일입니다. DNS 주소가 담겨 있습니다.                                                                                                                                                                              |
| `index.md`      | 사이트의 홈페이지 파일입니다. 홈페이지는 모든 포스트를 페이지 매김 변수의 수에 따라 시간 순서대로 나열합니다.                                                                                                                                                             |
| `README.md`     | 현재 보고 있는 파일입니다. 지킬 템플릿에 대한 설명이 담겨 있습니다.                                                                                                                                                                                                       |

---

참고한 사이트

- [Github Pages Docs](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll)
- [Jekyll Docs(EN)](https://jekyllrb.com/docs/)
- [Jekyll Docs(KR)](https://jekyllrb-ko.github.io/docs/)
- [Minimal Mistakes Guide](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/)

---

유용한 사이트

- [아이콘 검색](https://glyphsearch.com/)
- [font-awesome 전용 검색](https://fontawesome.com/icons)
- [Liquid](https://shopify.github.io/liquid/basics/introduction/)
