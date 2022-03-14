---
title: "Font Awesome 5"
categories:
  - Github
  - Pages
  - Guide
---

Github Pages에 기본적으로 동작하는 Jekyll은 Font Awesome 6를 지원합니다.

## 종류

Font Awesome의 종류는 Solid, Regular, Light, Brand가 있습니다.

```yaml
<i class='fas fa-fw fa-link'></i>
```

앞에 오는 fas를 보면 뒤에 s가 solid를 의미합니다.

`fa-fw`는 fixed width 옵션입니다. 해당 옵션을 사용하면 가로와 세로의 길이가 동일해 집니다. 고정폭 폰트를 생각하면 이해가 편합니다.

`fa-link`는 아이콘의 이름입니다.

계속 붙는 `fa`는 Font Awesome의 앞글자를 딴 약어입니다.

<i class='fas fa-fw fa-link'></i>

<i class="fas fa-fw fa-code-compare"></i>

## 스타일링

### 사이즈

```yaml
  <i class="fas fa-camera fa-xs"></i>
  <i class="fas fa-camera fa-sm"></i>
  <i class="fas fa-camera fa-lg"></i>
  <i class="fas fa-camera fa-2x"></i>
  <i class="fas fa-camera fa-3x"></i>
  <i class="fas fa-camera fa-5x"></i>
  <i class="fas fa-camera fa-7x"></i>
  <i class="fas fa-camera fa-10x"></i>
```

### 고정폭

```yaml

```

### List

```yaml
  <ul class="fa-ul">
    <li><span class="fa-li"><i class="fas fa-check-square"></i></span>List icons can</li>
    <li><span class="fa-li"><i class="fas fa-check-square"></i></span>be used to</li>
    <li><span class="fa-li"><i class="fas fa-spinner fa-pulse"></i></span>replace bullets</li>
    <li><span class="fa-li"><i class="far fa-square"></i></span>in lists</li>
  </ul>

```

### Rotate

```yaml
  <div class="fa-3x">
    <i class="fas fa-snowboarding"></i>
    <i class="fas fa-snowboarding fa-rotate-90"></i>
    <i class="fas fa-snowboarding fa-rotate-180"></i>
    <i class="fas fa-snowboarding fa-rotate-270"></i>
    <i class="fas fa-snowboarding fa-flip-horizontal"></i>
    <i class="fas fa-snowboarding fa-flip-vertical"></i>
    <i class="fas fa-snowboarding fa-flip-both"></i>
  </div>

```

### Animate

```yaml

```

### Border + Pull

```yaml

```

### Stack

```yaml

```
