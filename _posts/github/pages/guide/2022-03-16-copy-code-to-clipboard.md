---
title: "Github Pages Guide : 코드 블럭 복사하기 버튼 추가하기"

categories:
  - Github
  - Pages
  - Guide
---

지킬 블로그의 가장 큰 단점은 코드 블록에 기본적으로 복사-붙여넣기 기능이 존재하지 않는 점입니다. 이를 위해 직접 기능을 구현하는 방법에 대해 소개합니다.

## 버튼 배치

```html:_includes/codeHeader.html
<div class="code-header">
    <button class="copy-code-button" aria-label="Copy code to clipboard"></button>
</div>
```

```md
{% include codeHeader.html %}
```

