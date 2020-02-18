# 0214 Vue.js

## Table of Contents

1. [뷰 프로젝트 구성방법](#뷰-프로젝트-구성방법)
2. [Vue CLI](#Vue-CLI)
3. [Vue CLI를 활용한 프로젝트](#Vue-CLI를-활용한-프로젝트)
4. [시멘틱 태그](#시멘틱-태그)
5. [WAI-ARIA](#WAI-ARIA)



## 뷰 프로젝트 구성방법

### HTML 파일에서 Vue 코드를 작성하는 방식의 한계점 

HTML 파일에 여러 개의 컴포넌트를 등록하는 방식은 구문 강조가 되어 있지 않아 마크업이 어떻게 표현될지 예상하기 어렵다.

- 에디터나 IDE의 도움을 받을 수 없으므로 오탈자를 찾기 어려움
- 들여쓰기가 어려워 태그의 구조 및 관계를 파악하기 어려움

```javascript
// 컴포넌트 1
Vue.component('header', {
  template: `...`
})
// 컴포넌트 2
Vue.component('contents', { template: `...` })
// 컴포넌트 3
Vue.component('footer', { template: `...` })
```

### 싱글 파일 컴포넌트

싱글 파일 컴포넌트는 여러 개의 컴포넌트 및 template 속성을 추가할 경우 발생할 수 있는 가독성 문제를 해소해준다. 싱글 파일 컴포넌트는 `.vue`확장자 파일을 통해 프로젝트 구조를 구성하며 1개의 컴포넌트와 동일하다.

```html
<template>
	<!-- HTML -->
  <!-- 화면에 표시할 요소들을 정의하는 영역 -->
  <!-- HTML + Vue 데이터 바인딩 -->
</template>

<script>
export default {
  // Javascript
  // 뷰 컴포넌트의 내용을 정의하는 영역
  // template, data, methods
}	
</script>

<style>
	/* CSS */
  /* 템플릿에 추가된 HTML 태그의 스타일 속성 정의 */
</style>
```

#### 싱글 파일 컴포넌트 예제

```vue
<template>
<div>
	<button>{{ message }}</button>  
</div>
</template>

<script>
export default {
  data: {
    message: "click this button"
  }
}
</script>

<style>
  span {
    font-size: 1.2em;
  }
</style>
```

### Vetur 설치

VSCode의 Extensions에서 설치 가능

- Visual Studio Code에서 Vue 문법을 체크하는 툴
- Vue 문법에 따라 색상이 변하고, 기본 템플릿 코드도 만들어져 매우 편리

**[⬆ back to top](#table-of-contents)**

## Vue CLI

**Vue CLI 명령어를 통해 애플리케이션을 개발하기 위한 초기 구조를 쉽게 구성 가능하다**

- Vue CLI 명령어를 사용하여 생성한 프로젝트 템플릿을 통해 웹팩 같은 모듈 번들러를 프로젝트 자체에 포함하여 바로 사용할 수 있다.
- 템플릿은 `.vue`파일을 HTML, CSS JavaScript 파일로 변환해주는 Vue Loader를 포함하고 있다.

### 웹팩

싱글 파일 컴포넌트 체계를 사용하기 위해서는  `.vue`파일을 웹 브라우저가 인식할 수 있는 형태의 파일로 변환해야 한다. 이를 돕는 대표적인 도구로 웹팩(`Webpack`)이다. 웹팩(`Webpack`)은 웹 앱의 자원(HTML, CSS, 이미지)들을 자바스크립트 모듈로 변환해 하나로 묶어 웹의 성능을 향상시켜 주는 자바스크립트 모듈 번들러이다.

## Vue CLI를 활용한 프로젝트

### 뷰 CLI 설치

```bash
$ npm install vue-cli -global
```

### 뷰 CLI로 프로젝트 생성하기 

```bash
$ vue init webpack-simple
```

### 프로젝트 생성 후 Vue 앱을 구동하기 위한 라이브러리 다운로드

```bash
$ npm install
```

### Vue 앱 실행

>  생성 후에는 실행을 꼭 테스트해야 한다.

```bash
$ npm run dev
```

**[⬆ back to top](#table-of-contents)**
