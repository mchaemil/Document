# 0214 Vue.js

## Table of Contents

1. [뷰 프로젝트 구성방법](#뷰-프로젝트-구성방법)
2. [Vue CLI](#Vue-CLI)
3. [Vue CLI를 활용한 프로젝트](#Vue-CLI를-활용한-프로젝트)
4. [시멘틱 태그](#시멘틱-태그)
5. [WAI-ARIA](#WAI-ARIA)



## 뷰 프로젝트 구성 방법

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



## 시멘틱 태그 

시멘틱 태그를 통해 콘텐츠의 의미를 명시함으로써 브라우저, 검색엔진, 개발자는 이점을 얻을 수 있다. 

### 개발자가 얻는 이점

#### non-semantic 태그로 작성한 구조

```html
<div id="header">
  
</div>

<div id="container">
  <div class="article-setion">
  	<h2>내용의 제목</h2>
  </div>
  
</div>

<div id="footer">
  
</div>
```

#### semantic 태그로 작성한 구조

```html
<header>
	<!-- 제목, 로고, 목차  -->
</header>

<main>
  <section>
  	<h2>내용의 제목</h2>
  </section>

</main>

<footer>
	<!-- 하단 정보, 저작권  -->
</footer>
```

**개발자는 시멘틱 태그의 사용을 통해 코드의 가독성을 높이고 유지보수를 쉽게할 수 있는 장점을 얻는다.**

Vue에서 컴포넌트를 통해 각각의 역할과 기능을 분리했듯이 시멘틱 태그를 통해서 문서의 구조와 의미를 나눌 수 있다. 

아래는 HTML5에서 새롭게 추가된 시멘틱 태그이다.

| tag     | Description                                          |
| :------ | :--------------------------------------------------- |
| header  | 헤더를 의미한다                                      |
| nav     | 내비게이션을 의미한다                                |
| aside   | 사이드에 위치하는 공간을 의미한다                    |
| section | 본문의 여러 내용(article)을 포함하는 공간을 의미한다 |
| article | 분문의 주내용이 들어가는 공간을 의미한다             |
| footer  | 푸터를 의미한다                                      |

**[⬆ back to top](#table-of-contents)**



## WAI-ARIA

웹은 초기 문서 간의 연결을 위한 목적으로 설계되었지만 웹의 성정과 더불어 웹은 데스크탑 수준의 애플리케이션과 같은 사용자 경험을 요구하기에 이르렀다.

### RIA(Rich Internet Application)

Javascript의 성장과 Ajax의 등을 통해서 웹에서 데스크탑 수준의 애플리케이션과 같은 사용자 경험을 제공할 수 있게 되었고,  RIA를 등장시켰다.  RIA의 등장은 역동적이고 화려하고 편리한 UX를 제공하지만 모든 사용자가 동등하게 접근할 수 없는 문제가 생긴다.

장애인, 시각 장애인, 정보 접근성 약자들은 스크린 리더 등 보조기술을 사용하더라도 RIA기술로 제작된 웹 애플리케이션을 제대로 사용할 수 없다는 문제가 생긴다.

### WAI-ARIA (Web Accessibility Initiative - Web Accessible Rich Internet Applications)

W3C에서 웹 콘텐츠 및 웹 애플리케이션의 접근성을 개선하기 위한 명세인 **WAI-ARIA** 발표했다. **WAI-ARIA**는 마크업에 역할, 속성, 상태의 정보를 추가할 수 있도록 지원한다. 

```vue
<span class="addContainer" v-on:click="addTodo">
	<i class="fa fa-plus" aria-hidden="true"></i>
</span>
```

HTML 태그에 `aria-hidden="true"`를 지정하면 스크린 리더 등의 보조기기에서 의미적으로 숨긴 콘텐츠로 인식하여, 스크린 리더의 가상 커서로 요소를 탐색할 수 없게 된다.

| 속성  | 의미                                                         |
| ----- | ------------------------------------------------------------ |
| true  | 스크린 리더와 같은 보조기술 사용자의 콘텐츠 탐색을 제한하며, 가상 커서에 탐색되지 않음 |
| false | 스크린 리더 같은 보조기술 사용자에게 숨겨진 콘텐츠를 노출하여, 가상 커서를 통한 탐색을 허용 |

**[⬆ back to top](#table-of-contents)**
