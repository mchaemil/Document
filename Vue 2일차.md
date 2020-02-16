## 목차

1. 뷰라우터
2. 뷰 HTTP 통신
   1. 웹 앱의 HTTP 통신방법
   2. axios
3. 뷰템플릿
   
   

---



## 뷰 라우터

### 라우팅(Routing)은 라우터(Router)를 이해하기 위한 선행 개념이므로 중요

라우팅이란 웹 페이지 간의 이동 방법을 말하며, SPA(Single Page Application)에서 주로 사용된다. 라우팅을 사용하면 깜빡거림 없이 화면을 매끄럽게 전환할 수 있으며, 사용자 경험을 향상할 수 있다.

### 뷰 라우터

뷰 라우터는 뷰에서 라우팅 기능을 구현할 수 있도록 지원하는 공식 라이브러리이다. 

```html
<script src="https://unpkg.com/vue-router/dist/vue-router.js"></script>
```

| 태그                        | 설명                                                         |
| --------------------------- | ------------------------------------------------------------ |
| `<router-link to="URL 값">` | 페이지 이동 태그, 화면에서는 <a>로 표시되며, `to`에 지정한 URL로 이동함 |
| `<router-view>`             | 페이지 표시 태그, 변경되는 URL에 따라 해당 컴포넌트를 뿌려주는 영역 |

### $mount() API란?

`$mount()` API는 `el` 속성과 동일하게 인스턴스를 화면에 붙이는 역할을 하며, 인스턴스를 생성할 때 `el`을 넣지 않았더라도 생성하고 나서 `$mount()`를 이용하면 강제로 인스턴스를 화면에 붙일 수 있다. 참고로, 뷰 라우터의 공식 문서는 모두 인스턴스 안에 `el`을 지정하지 않고, 생성된 인스턴스를 `$mount()`를 이용해 붙이는 식으로 안내하고 있다.

### 중첩된 라우트(Nested Router)

중첩된 라우트(Nested Router)는 라우터로 페이지를 이동할 때 최소 2개 이상의 컴포넌트를 화면에 나타낼 수 있다. 중첩된 라우트(Nested Router)를 사용하면 URL에 따라서 컴포넌트의 하위 컴포넌트가 다르게 표시된다.

```
/user/foo/profile                     /user/foo/posts
+------------------+                  +-----------------+
| User             |                  | User            |
| +--------------+ |                  | +-------------+ |
| | Profile      | |  +------------>  | | Posts       | |
| |              | |                  | |             | |
| +--------------+ |                  | +-------------+ |
+------------------+                  +-----------------+
```

중첩된 라우트 구성을 통해 URL에 따라 하위 컴포넌트가 바뀌더라도 위와 같은 관계를 표현할 수 있다.

### 네임드 뷰(Named View)

특정 페이지로 이동했을 때 여러 개의 컴포넌트를 동시에 표시하는 라우팅 방식이다. URL에 맞추어 같은 레벨에서 여러 개의 컴포넌트를 한 번에 표시할 때 사용한다. 

### 네임드 뷰 예제

```html
<div id="app">
  <router-view name="header"></router-view>
  <router-view></router-view>
  <router-view name="footer"></router-view>
</div>
```

```javascript
var Body = {template: '<div>This is Body</div>'}
var Header = {template: '<div>This is Body</div>'}
var Footer = {template: '<div>This is Body</div>'}

var router = new VueRouter({
  routes: [
    path:'/',
    components: {
    	default: Body,
    	header: Header,
    	footer: Footer
    }
  ]
})

var app = new Vue({
  el:'#app',
  router: router
})
```



## 뷰 HTTP 통신

### 웹 앱의  HTTP 통신 방법

웹 앱에서 서버에 데이터를 요청하는 HTTP 통신은 필수로 구현해야 하는 기능이며, 이를 통해 사용자와 상호 작용에 따라 데이터를 동적으로 화면에 표시할 수 있다.

뷰에서도 ajax를 지원하기 위한 라이브러리를 제공하며, 뷰 리소스와 엑시오스(axios)가 있다. 

### axios 

`axios`는 뷰 커뮤니티에서 가장 많이 사용되는 HTTP 통신 라이브러리이다. 엑시오스는 Promise기반의 API 형식이 다양하게 제공되어 별도의 로직을 구현할 필요 없이 주어진 API만으로도 간편하게 원하는 로직을 구현할 수 있다.

| API 유형                                | 처리 결과                                                    |
| --------------------------------------- | ------------------------------------------------------------ |
| `axios.get('URL 주소').then().catch()`  | 해당 URL 주소에 대해 HTTP GET 요청을 보낸다. 서버에서 보낸 데이터를 정상적으로 받아오면 then()안에 정의한 로직이 실행되고, 오류가 발생하면 catch()에 정의한 로직이 수행 |
| `axios.post('URL 주소').then().catch()` | 해당 URL 주소에 대해 HTTP POST 요청을 보내며, 기본적인 동작은 get()과 동일 |
| `axios({ 옵션 속성 })`                  | HTTP 요청에 대한 자세한 속성들을 직접 정의하여 보낼 수 있다 데이터 요청을 보낼 URL, HTTP 요청방식, 보내는 데이터 유형, 기타 등등 |

```html
<script src="https://unpkg.com/axios/dist/axios.min.js"></script> <!-- axios CDN -->
```

```javascript
new Vue({
  el: '#app',
  methods: {
    getData() {
			axios.get('https://raw.githubusercontent.com/joshua1988/doit-vuejs/master/data/demo.json')
      .then(res => {
        console.log(res)
        console.log(res.data)        
      })
    
    }
  }
})
```



## 뷰 템플릿

### 뷰 템플릿이란?

**뷰 템플릿**이란 HTML, CSS 등의 마크업 속성과 뷰 인스턴스에서 정의한 데이터 및 로직들을 연결하여 **사용자가 브라우저에서 볼 수 있는 형태의 HTML로 변환해주는 속성**이다. 



### 데이터 바인딩

#### {{ }} - 콧수염 괄호

`{{}}`는 뷰 인스턴스의 데이터를 HTML 태그에 연결하는 가장 기본적인 텍스트 삽입 방식이다.  뷰 인스턴의 데이터를 HTML에서 표현하기 위해 사용한다.

#### v-bind

`v-bind`는 `id`, `class`, `style` 등의 HTML 속성 값에 뷰 데이터의 값을 연결할 때 사용하는 데이터 연결 방식이며, `v-bind` 속성으로 지정할 HTML 속성이나 props 속성 앞에 접두사로 붙인다.

```javascript
new Vue({
  el:'#app',
  data: {
		idA: 10,
    classA: 'container',
    styleA: 'color: blue',
  }
})
```

뷰 코드가 전반적으로 `v-` 접두사를 붙이는 형태이므로 가급적 `v-bind` 속성을 이용하는 것이 HTML 문법과 구분도 되고, 다른 사람이 코드를 파악하기도 쉽다.

### 자바스크립트 표현식

뷰의 템플릿에서도 자바스크립트 표현식을 사용할 수 있지만 아래와 같은 사항에 대해서 주의해야 한다.

1. 자바스크립트 선언문과 분기문은 사용할 수 없음
2. 복잡한 연산은 인스턴스 안에서 처리, 화면과 로직을 분리해야 함

```html
<div id="#app">
  {{ true ? 100 : 0 }}
</div>
```



### 디렉티브

뷰 디렉티브란 HTML 태그 안에 `v-` 접두사를 가지는 모든 속성들을 말하며 예시는 아래와 같다.

```html
<a v-if="isTrue"></a>
```

| 디렉티브 이름 | 역할                                                         |
| ------------- | ------------------------------------------------------------ |
| `v-if`        | 지정한 뷰 데이터 값의 참, 거짓 여부에 따라 해당 HTML 태그를 화면에 표시하거나 표시하지 않음 |
| `v-for`       | 지정한 뷰 데이터의 개수만큼 해당 HTML 태그를 반복 출력       |
| `v-show`      | `v-if`와 유사하지만 데이터의 참, 거짓 여부에 따라 해당 HTML 태그를 화면에 표시하거나 표시하지 않음 |
| `v-bind`      | HTML태그의 기본 속성과 뷰 데이터 속성을 연결                 |
| `v-on`        | 화면 요소의 이벤트를 감지하여 처리할 때 사용                 |
| `v-model`     | 폼(`form`)에서 주로 사용되는 속성으로 폼에 입력한 값을 뷰 인스턴스의 데이터와 즉시 동기화할 수 있고, 화면에 입력된 값을 저장하여 서버에 보내거나 `watch`같은 고급 속성을 이용하여 추가 로직을 수행 |



### 이벤트 처리

뷰에서는 화면에서 발생한 이벤트를 처리하기 위해 `v-on` 디렉티브와 `methods` 속성을 활용

```html
<button v-on:click="clickBtn">클릭</button>
```

```javascript
methods: {
  clickBtn() {
    alert('clicked');
  }
}
```

#### 디렉티브로 메서드 호출시 인자값 넘기기

디렉티브로 메서드 호출시 인자값을 넘기는 행위는 옳지 않다.   

**화면과 로직을 분리해야 한다.**

```html
<button v-on:click="clickBtn(10)">클릭</button>
```

```javascript
methods: {
  clickBtn(num) {
    alert('clicked ' + num + ' times');
  }
}
```



### 고급 템플릿 기법 

#### computed 속성

HTML에 `{{ }}`를 사용해 데이터를 바인딩할 수도 있지만 `computed 속성`을 사용하면 아래와 같은 이점을 얻을 수 있다.

1. data 속성 값의 변화에 따라 자동으로 연산
2. **캐싱**, 즉 동일한 연산을 반복하지 않기 위해 연산의 결과값을 미리 저장해놓고, 필요할 때 불러오는 동작

```javascript
new Vue({
  el:'#app',
  data: {
    message: 'Hello Vue.js!'
  },
  computed: {
  	reversedMessage() { // reversedMessage가 미리 연산결과를 가지고 있음
      return this.message.split('').reverse().join('') // 결과만 표시
    }  
  }
})
```













