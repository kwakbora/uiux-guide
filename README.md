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

