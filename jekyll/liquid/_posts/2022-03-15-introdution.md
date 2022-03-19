---
title: "Liquid : 소개"
excerpt: "Liquid를 다루는 데 필요한 기본적인 연산자 등을 알아보자"
header:
  actions:
    - label: "<i class='fas fa-fw fa-link'></i> Liquid 더 알아보기"
      url: "https://jinhyun.blog/liquid/"
---

## 객체

**객체**에는 Liquid가 페이지에 표시하는 콘텐츠가 포함됩니다. 이중 중괄호({% raw %}`{{`, `}}`{% endraw %})로 묶이면 객체와 변수가 표시됩니다.

**Input**:

{% raw %}

```md
{{ page.title }}
```

{% endraw %}

**Output**:

```md
{{ page.title }}
```

이 경우 Liquid는 '{{ page.title }}'라는 텍스트가 포함된 페이지 객체의 title 속성을 렌더링합니다.

## 태그

**태그**는 템플릿에 대한 논리 및 제어 흐름을 생성합니다.

중괄호, 퍼센트 기호로 표현합니다.

{% raw %}

```md
{% %}
```

{% endraw %}

태그 안 텍스트는 템플릿이 렌더링될 때 가시적인 출력을 생성하지 않습니다.

이를 통해 페이지에 Liquid 로직을 표시하지 않고 변수를 할당하고 조건 또는 루프를 생성할 수 있습니다.

**Input**:

{% raw %}

```md
{% if site.name %}
  Hello {{ site.name }}!
{% endif %}
```

{% endraw %}

**Output**:

{% if site.name %}
  Hello {{ site.name }}!
{% endif %}

태그는 다음과 같이 분류됩니다.

- [흐름 제어 (Control flow)]({{ site.url }}/liquid/control-flow/)
- [반복 (Iteration)]({{ site.url }}/liquid/iteration/)
- [템플릿 (Template)]({{ site.url }}/liquid/template/)
- [변수 할당 (Variable assignment)]({{ site.url }}/liquid/variable-assignment/)

각 태그 유형에 대한 자세한 내용은 해당 섹션에서 확인할 수 있습니다.

## 필터

**필터**는 Liquid 객체 또는 변수의 출력을 변경합니다.

이중 중괄호 및 변수 할당 내에서 사용되며 파이프 문자 `|`로 구분됩니다.

**Input**:

{% raw %}

```md
{{ "/my/fancy/url" | append: ".html" }}
```

{% endraw %}

**Output**:

{{ "/my/fancy/url" | append: ".html" }}

하나의 출력에 여러 필터를 사용할 수 있으며 왼쪽에서 오른쪽으로 적용됩니다.

**Input**:

{% raw %}

```md
{{ "adam!" | capitalize | prepend: "Hello " }}
```

{% endraw %}

**Output**:

{{ "adam!" | capitalize | prepend: "Hello " }}
