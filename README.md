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

```html
.
├── _config.yml
├── _data
│   └── members.yml
├── _drafts
│   ├── begin-with-the-crazy-ideas.md
│   └── on-simplicity-in-technology.md
├── _includes
│   ├── footer.html
│   └── header.html
├── _layouts
│   ├── default.html
│   └── post.html
├── _posts
│   ├── 2007-10-29-why-every-programmer-should-play-nethack.md
│   └── 2009-04-26-barcamp-boston-4-roundup.md
├── _sass
│   ├── _base.scss
│   └── _layout.scss
├── _site
├── .jekyll-metadata
└── index.html # 올바른 머리말을 가진 'index.md' 도 가능
```

각 파일과 디렉토리가 하는 일의 개요는 다음과 같습니다:

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>파일 / 디렉토리</th>
      <th>설명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p><code>_config.yml</code></p>
      </td>
      <td>
        <p>
          <a href="/docs/configuration/">환경설정</a> 정보를 보관한다. 명령어를
          실행할 때 여러가지 옵션들을 추가할 수도 있지만, 그렇게 따로 외우는
          것보다 이 파일에 정의해두는게 더 편리하다.
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>_drafts</code></p>
      </td>
      <td>
        <p>
          초안이란 아직 게시하지 않은 포스트를 말한다. 파일명 형식에 날짜가
          없다: <code>title.MARKUP</code>. 사용 방법은 <a href="/docs/posts/#drafts">
          초안 활용하기</a>를 참고하라.
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>_includes</code></p>
      </td>
      <td>
        <p>
          재사용하기 위한 파일을 담는 디렉토리로서, 필요에 따라 포스트나
          레이아웃에 쉽게 삽입할 수 있다.
          <code>{% raw %}{% include file.ext %}{% endraw %}</code> 와 같이
          Liquid 태그를 사용하면 <code>_includes/file.ext</code> 파일에 담긴
          코드가 삽입된다.
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>_layouts</code></p>
      </td>
      <td>
        <p>
          포스트를 포장할 때 사용하는 템플릿이다. 각 포스트 별로
          레이아웃을 선택하는 기준은
          <a href="/docs/front-matter/">머리말</a>이며, 자세한 내용은 다음
          섹션에서 설명한다.
          <code>{% raw %}{{ content }}{% endraw %}</code> 와 같이 Liquid 태그를
          사용하면 페이지에 컨텐츠가 주입된다.
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>_posts</code></p>
      </td>
      <td>
        <p>
          한마디로 말하면, 당신의 컨텐츠다. 중요한 것은 파일들의 명명규칙인데,
          반드시 이 형식을 따라야 한다:
          <code>YEAR-MONTH-DAY-title.MARKUP</code>.
          <a href="/docs/permalinks/">고유주소</a>는 포스트 별로 각각 정의할 수
          있지만, 날짜와 마크업 언어 종류는 오로지 파일명에 의해
          결정된다.
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>_data</code></p>
      </td>
      <td>
        <p>
<!--
          Well-formatted site data should be placed here. The Jekyll engine
          will autoload all data files (using either the <code>.yml</code>,
          <code>.yaml</code>, <code>.json</code>, <code>.csv</code> or
          <code>.tsv</code> formats and extensions) in this directory,
          and they will be accessible via `site.data`. If there's a file
          <code>members.yml</code> under the directory, then you can access
          contents of the file through <code>site.data.members</code>.
-->
          사이트에 사용할 데이터를 적절한 포맷으로 정리하여 보관하는 디렉토리.
          Jekyll 엔진은 이 디렉토리에 있는 (확장자와 포맷이 <code>.yml</code>
          또는 <code>.yaml</code>, <code>.json</code>, <code>.csv</code>,
          <code>.tsv</code> 인) 모든 데이터 파일을 자동으로 읽어들여
          `site.data` 로 사용할 수 있도록 만든다. 만약 이 디렉토리에
          <code>members.yml</code> 라는 파일이 있다면,
          <code>site.data.members</code> 라고 입력하여 그 컨텐츠를 사용할 수 있다.
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>_sass</code></p>
      </td>
      <td>
        <p>
<!--
          These are sass partials that can be imported into your <code>main.scss</code>
          which will then be processed into a single stylesheet
          <code>main.css</code> that defines the styles to be used by your site.
-->
          이것은 당신의 <code>main.scss</code> 에 임포트할 수 있는 Sass 조각들로서,
          하나의 스타일시트 파일 <code>main.css</code> 로 가공되어 당신의 사이트에서
          사용하는 스타일들을 정의한다.
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>_site</code></p>
      </td>
      <td>
        <p>
<!--
          This is where the generated site will be placed (by default) once
          Jekyll is done transforming it. It’s probably a good idea to add this
          to your <code>.gitignore</code> file.
-->
          Jekyll 이 변환 작업을 마친 뒤 생성된 사이트가 저장되는 (디폴트)
          경로이다. 대부분의 경우, 이 경로를 <code>.gitignore</code> 에
          추가하는 것은 괜찮은 생각이다.
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>.jekyll-metadata</code></p>
      </td>
      <td>
        <p>
<!--
          This helps Jekyll keep track of which files have not been modified
          since the site was last built, and which files will need to be
          regenerated on the next build. This file will not be included in the
          generated site. It’s probably a good idea to add this to your
          <code>.gitignore</code> file.
-->
          Jekyll 은 이 파일을 참고하여, 마지막으로 빌드한 이후에 한번도 수정되지
          않은 파일은 어떤 것인지, 다음 빌드 때 어떤 파일을 다시 생성해야 하는지
          판단할 수 있다. 생성된 사이트에 이 파일이 복사되지는 않는다. 대부분의
          경우, 이 파일을 <code>.gitignore</code> 에 추가하는 것은 괜찮은
          생각이다.
        </p>
      </td>
    </tr>
    <tr>
      <td>
<!--
        <p><code>index.html</code> or <code>index.md</code> and other HTML,
        Markdown files</p>
-->
        <p><code>index.html</code> 또는 <code>index.md</code> 및 다른 HTML,
        마크다운 파일</p>
      </td>
      <td>
        <p>
<!--
          Provided that the file has a <a href="/docs/front-matter/">front
          matter</a> section, it will be transformed by Jekyll. The same will
          happen for any <code>.html</code>, <code>.markdown</code>,
          <code>.md</code>, or <code>.textile</code> file in your site’s root
          directory or directories not listed above.
-->
          Jekyll 은 <a href="/docs/front-matter/">머리말</a> 섹션을 가진 모든
          파일을 찾아 변환 작업을 수행한다. 위에서 언급하지 않은 다른 디렉토리나
          사이트의 루트 디렉토리에 있는 모든 <code>.html</code>,
          <code>.markdown</code>, <code>.md</code>, <code>.textile</code> 이
          여기에 해당한다.
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>다른 파일/폴더</p>
      </td>
      <td>
        <p>
          <code>css</code> 나 <code>images</code> 폴더, <code>favicon.ico</code>
          파일같이 앞서 언급하지 않은 다른 모든 디렉토리와 파일들은 있는 그대로
          생성된 사이트에 복사한다. 다른 사람들이 만든 사이트는 어떤식으로
          생겼는지 궁금하다면, <a href="/showcase/">Jekyll 을 사용하는
          사이트들</a>이 이미 많이 있으니 살펴보도록 한다.
        </p>
      </td>
    </tr>
  </tbody>
</table>
</div>

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
