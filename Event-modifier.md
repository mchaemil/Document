# Event 수식어

이벤트가 발생하면 크롬이나 파이어폭스 같은 브라우저는 bubble, capture, target 이라는 3가지 방법을 이용해 어디에서 이벤트가 발생했는지 찾는다.

## Bubble

bubble은 이벤트가 발생한 대상 엘리먼트에서 부모, 조상 엘리먼트 형태로 진행되며, 이를 이벤트 버블링이라고 한다. 

### 예시

```html
<div id="app">
  <div class="container">
    <div id="outer" class="blue white-text" @click="handleClickEvent">
      Outer
      <div id="middle" class="yellow" @click="handleClickEvent">
        Middle
        <div id="inner" class="cyan" @click="handleClickEvent">
          Inner
        	<button id="button" @click="handleClickEvent">클릭</button>
        </div>
      </div>
    </div>
  </div>
</div>
```

```javascript
methods: {
	handleClickEvent() {
    console.log(`handleClickEvent target: ${$event.target.id}`+ ` currentTarget: ${$event.currentTarget.id}`)
  }
}
```

 ![bubble button](https://user-images.githubusercontent.com/40027211/74607245-8f18fb00-511a-11ea-812d-f472142f241c.PNG)

### 각각의 영역을 클릭할 경우 콘솔창 확인

![complexBubbling](https://user-images.githubusercontent.com/40027211/74607605-97266a00-511d-11ea-8864-cd56ba0541f8.PNG)



### DOM 요소 비교를 통해서 로직을 실행하는 방법

```javascript
methods: {
  handleClickEvent(event) {
    if (event.target.nodeName.toLowerCase() === 'button') {
      // 해당 요소일 경우 특정 로직을 수행
      console.log('버튼입니다.')
    } else {
      console.log(`handleClickEvent target: ${$event.target.id}`+ ` currentTarget: ${$event.currentTarget.id}`)
    }
  }
}
```



![bubble button](https://user-images.githubusercontent.com/40027211/74607245-8f18fb00-511a-11ea-812d-f472142f241c.PNG)

### v-on 디렉티브 수식어

| 설명              | 기능                                                         |
| ----------------- | ------------------------------------------------------------ |
| stopPropagation() | 이벤트 버블링을 중지                                         |
| stop              | 이벤트 버블링을 중지                                         |
| prevent           | 브라우저가 이벤트 발생 시 기본적으로 발생하는 동작을 중지. 대표적으로 submit이나 앵커 태그의 클릭 이후 발생할 이벤트를 중지하는데 사용 |
| capture           | 이벤트 버블링과 반대되는 동작을 수행                         |
| self              | 이벤트가 전파되지 않고 자신에서만 이벤트가 발생              |
| once              | 이벤트가 한 번만 발생                                        |
| passive           | 휴대폰 같은 터치 이벤트 기반의 수동적인 이벤트 리스닝 성능 향상에 활용 |



### stopPropagation 예시

![bubble button](https://user-images.githubusercontent.com/40027211/74607245-8f18fb00-511a-11ea-812d-f472142f241c.PNG)

```javascript
methods: {
	handleClickEvent() {
    $event.stopPropagation();
    console.log(`handleClickEvent target: ${$event.target.id}`+ ` currentTarget: ${$event.currentTarget.id}`)
  }
}
```

![stopPropagation](https://user-images.githubusercontent.com/40027211/74607565-3ac34a80-511d-11ea-98f6-35e19d12de3b.PNG)



## Storage

![push-one-Object](https://user-images.githubusercontent.com/40027211/74607721-6d217780-511e-11ea-9f43-09512fd20928.PNG)

> Web Storage API는 브라우저에서 쿠키를 사용하는 것보다 훨씬 직관적으로 key/value 데이터를 안전하게 저장할 수 있는 메커니즘을 제공합니다.   
> [참고 - MDN Web Storage API](https://developer.mozilla.org/ko/docs/Web/API/Web_Storage_API/Using_the_Web_Storage_API)



### localStorage와 sessionStorage

window객체 안에는 `localStorage`와 `sessionStorage`라는 저장소가 있다. 두 스토리지는 HTML5에서 추가된 저장소이며, key/value형태로 데이터를 저장하는 Storage이다.

`localStorage`와 `sessionStorage`는 `Storage`객체를 상속받으므로 메소드가 공통적으로 존재한다. 이 둘은 데이터를 영구적으로 보존하는지 아닌지에 따라서 차이를 가지게 되는데, `localStorage`는 사용자가 데이터를 제거하지 않는 이상 영구적으로 남는 반면, `sessionStorage`의 경우 윈도우를 종료하거나 브라우저 탭을 닫을 경우 데이터가 제거된다. 

| 종류             | 설명                                                         |
| ---------------- | ------------------------------------------------------------ |
| `localStorage`   | `localStorage`는 사용자가 데이터를 제거하지 않는 이상 영구적으로 존재 |
| `sessionStorage` | 윈도우를 종료하거나 브라우저 탭을 닫을 경우 데이터가 제거    |



### localStorage

`localStorage` 객체는 단순한 key/value만을 저장하는 저장소이며, 객체와 비슷하다. 다만 중요한 점은 이 데이터들이 페이지 로딩 이후에도 온전히 유지된다는 점이다.

`localStorage`에 저장하는 `key`와 `value`는 문자열로 변환된다. boolean이나 정수 같은 기본형 타입의 데이터를 저장한다고 해도 자동으로 string으로 변경된다

### Storage 메서드

| 속성                 | 설명                                               |
| -------------------- | -------------------------------------------------- |
| Storage.setItem()    | 인자로 key, value를 전달해 Storage에 저장          |
| Storage.getItem()    | 인자로 key를 전달하여 Storage에 저장된 값을 조회   |
| Storage.removeItem() | 인자로 key을 전달하면 해당 키가 Storage에서 지워짐 |
| Storage.clear()      | Storage 전체를 비움                                |


### localStorage에 데이터 넣어보기
`localStorage`에 데이터를 저장할 때 key/value 형식으로 저장할 수도 있지만, 객체 형태로 저장하려면 `JSON.stringify()`를 통해 객체 타입을 문자열 타입으로 변환하여 저장해야 한다. 또한 반대로 `localStorage`의 데이터를 가져올 때는 `JSON.parse()`를 통해 문자열을 객체 타입으로 변환하여 가져와야 한다.

```javascript
const TODOS_LS = "toDos";
const toDos = [];

for (let i = 0; i < 5; i++) {
  const toDoObj = {
    text:"안녕하세요",
    id: i + 1
  }
  toDos.push(toDoObj);  
}

localStorage.setItem(TODOS_LS, JSON.stringify(toDos))
```

### 

## JSON

JSON(JavaScript Object Notation)은 자바스크립트 문법의 데이터 교환 형식이다. 일반 자바스크립트 문법을 사용하며, 숫자, 불린, 배열, 객체까지 허용된다.  다만 작은 따옴표는 허용하지 않으며, `key`도 쌍따옴표로 감싸져야 한다.

```javascript
{
  "title": "JSON",
  "author": "me",
  "private": true,
}
```

### JSON 객체

| 메소드    | 설명                                                    |
| --------- | ------------------------------------------------------- |
| stringify | 인자로 전달된 자바스크립트 `object`를 `string`으로 변환 |
| parse     | 인자로 전달된 string을 자바스크립트 object로 변환       |



### JSON.stringify

`localStorage.setItem(TODOS_LS, toDos)`처럼 `setItem()`메소드의 인자에 자바스크립트 데이터를 직접 넣으면 `LocalStorage`에는 `[object Object]`처럼 데이터가 들어간다.

왜냐하면 `LocalStorage`에는 자바스크립트의 data를 저장할 수 없기 때문이다. `LocalStorage`는 모든 데이터를 `string`으로 저장한다. 그래서 자바스크립트 `object`가 `string`이 되도록 바꾸고 저장해야 한다. 이를 위해서 `JSON.stringify()`메소드를 사용해야 하는데, `JSON.stringify()`는 인자로 전달된 자바스크립트 `object`를 `string`으로 바꿔준다.

```javascript
function saveToDoList(){
  localStorage.setItem(TODOS_LS, JSON.stringify(toDos));
}
```

### JSON.parse

`localStorage.getItem()`으로 데이터를 불러온 경우 불러온 데이터가 `string`이라는 문제가 생긴다! 이를 자바스크립트에서 활용하기 위해서는 `JSON.parse`를 통해 string을 object로 변환해야 한다.

아래는 `localStorage`에서 가져온 코드를 `JSON.parse()`메서드를 통해 `string`을 `object`로 바꾸었다.

```javascript
function loadToDoList() {
  const loadedToDos = localStorage.getItem(TODOS_LS);
  if(loadedToDos !== null) {
    const parsedToDos = JSON.parse(loadedToDos);
    parsedToDos.forEach(todo => {
      console.log(todo.text);
    });
  } 
}
```







## 참고

[JSON - 제로초](https://www.zerocho.com/category/JavaScript/post/57432adfa48729787807c3fb)
