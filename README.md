# Sass 설치하기
1. 전역설치(Node.js필요)
  ```bash
  npm install -g sass
  ```

2. 프로젝트 로컬 설치
  ```bash
  npm install --save-dev sass
  ```

# SCSS 폴더 구조 예시
```bash
scss/
│── abstracts/   // 변수, 함수, 믹스인, placeholder (프로젝트 전역에서 재사용되는 로직)
│── base/        // reset, typography, 기본 스타일 (html, body, a 등)
│── components/  // 버튼, 카드, 모달 같은 컴포넌트 단위 스타일
│── layout/      // 헤더, 푸터, 네비게이션, 그리드, 레이아웃 관련
│── pages/       // 개별 페이지 전용 스타일 (home, about 등)
│── main.scss    // 위의 모든 partial을 import하는 엔트리 파일
```

## [각 폴더 역할]
● abstracts → _variables.scss, _mixins.scss, _functions.scss, _placeholders.scss

● base → _reset.scss, _typography.scss, _base.scss

● components → _button.scss, _card.scss, _modal.scss …

● layout → _header.scss, _footer.scss, _grid.scss, _navigation.scss

● pages → 개별 페이지 전용 스타일 (home, about 등)


## main.scss 예시
main.scss → main.css 로 빌드되게끔 Sass 컴파일러를 설정해 두면 좋아요.
- 실시간 감시(SCSS 파일이 수정될 때마다 자동으로 다시 컴파일됩니다.)
  ```bash
  sass --watch scss/main.scss dist/main.css
  ```
// abstracts

@import 'abstracts/variables';

@import 'abstracts/mixins';

// base

@import 'base/reset';

@import 'base/typography';

@import 'base/base';


// layout

@import 'layout/header';

@import 'layout/footer';


// components

@import 'components/button';

@import 'components/card';


// pages

@import 'pages/home';


## _variables.scss(CSS 변수 버전 예시)
```bash
:root {
  /* Colors */
  --color-primary: #3498db;
  --color-secondary: #2ecc71;
  --color-accent: #e74c3c;

  --color-text: #333;
  --color-bg: #f9f9f9;

  /* Fonts */
  --font-family-base: 'Arial', sans-serif;
  --font-size-base: 16px;

  --font-size-h1: 2.5rem;
  --font-size-h2: 2rem;
  --font-size-h3: 1.5rem;

  /* Spacing */
  --spacing-xs: 4px;
  --spacing-sm: 8px;
  --spacing-md: 16px;
  --spacing-lg: 24px;
  --spacing-xl: 40px;

  /* Breakpoints */
  --breakpoint-sm: 576px;
  --breakpoint-md: 768px;
  --breakpoint-lg: 992px;
  --breakpoint-xl: 1200px;
}

/* 다크모드 지원 */
[data-theme="dark"] {
  --color-primary: #9b59b6;
  --color-secondary: #16a085;
  --color-accent: #c0392b;

  --color-text: #eee;
  --color-bg: #222;
}
```

### css변수(--) 를 사용하는 이유
- Sass 변수($)

1. 빌드(컴파일)할 때만 쓰임

2. 최종 CSS에는 값으로만 남음

3. 브라우저, JS에서는 접근 불가 (정적)

- CSS 변수(--)

1. 최종 CSS에 그대로 남음

2. 브라우저 런타임에서 읽고 수정 가능

3. 다크모드, 사용자 테마, JS 동적 제어에 유리 (동적)


## 실무에서 많이 사용하는 _mixins.scss 예시
```bash
// 반응형 미디어쿼리
@mixin respond-to($breakpoint) {
  @if $breakpoint == sm {
    @media (min-width: 576px) { @content; }
  } @else if $breakpoint == md {
    @media (min-width: 768px) { @content; }
  } @else if $breakpoint == lg {
    @media (min-width: 992px) { @content; }
  } @else if $breakpoint == xl {
    @media (min-width: 1200px) { @content; }
  }
}

// Flex 유틸리티
@mixin flex($justify: flex-start, $align: stretch, $direction: row) {
  display: flex;
  justify-content: $justify;
  align-items: $align;
  flex-direction: $direction;
}

// 버튼 스타일
@mixin button($bg, $color: #fff, $radius: 4px) {
  background-color: $bg;
  color: $color;
  border: none;
  border-radius: $radius;
  padding: 0.5rem 1rem;
  cursor: pointer;
  transition: 0.3s;

  &:hover {
    opacity: 0.9;
  }
}

// 트랜지션
@mixin transition($property: all, $duration: 0.3s, $ease: ease-in-out) {
  transition: $property $duration $ease;
}

// 텍스트 줄임말 (ellipsis)
@mixin ellipsis($lines: 1) {
  display: -webkit-box;
  -webkit-line-clamp: $lines;
  -webkit-box-orient: vertical;
  overflow: hidden;
  text-overflow: ellipsis;
}

// 컨테이너 max-width + margin auto
@mixin container($max-width: 1200px) {
  width: 100%;
  max-width: $max-width;
  margin-left: auto;
  margin-right: auto;
  padding-left: 16px;
  padding-right: 16px;
}
```

### 사용예시
```bash
@import 'abstracts/mixins';
@import 'abstracts/variables';

.container {
  @include container();
}

.header {
  @include flex(space-between, center);
}

.button-primary {
  @include button($primary);
}

.card {
  @include transition(transform, 0.2s);
  &:hover {
    transform: translateY(-5px);
  }
}

.post-title {
  @include ellipsis(2);
}

.main {
  @include respond-to(md) {
    padding: 32px;
  }
}

```
