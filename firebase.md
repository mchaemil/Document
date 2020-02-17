# Firebase



## Firebase 장점 

- 사용하기 쉬운 개발도구로서
  - 사용하기 쉽게 개발 문서가 되어 있음
  - 직관적인 API
- 다양한 플랫폼을 지원한다.
  - iOS, Android, Web 플랫폼 지원 
- 통합된 개발환경
  - 하나의 SDK, 하나의 콘솔이 존재하며, 개발 가이드나 API를 참조할 때 찾아봐야할 사이트도 한 곳으로 통합되어 있음
  - 각 기능들 사이에 데이터 흐름을 한 눈에 파악할 수 있음
- Cloud Messaging을 통해 iOS, Android, Web 등 플랫폼을 넘나들며 사용자에게 메시지와 알림을 무료로 보냄 
- Hosting 최신형 웹 앱을 위해 맞춤 제작된 도구로 웹 호스팅을 단순화
- 인증
  - 이메일 및 비밀번호, 타사 제공업체, 기존 계정 시스템 직접 사용 등의 다양한 인증 방법을 제공
- 데이터 베이스(Real Time)
  - 클라이언트 간에 동기화된 상태를 실시간으로 요구하는 모바일 앱을 위한 효율적이고 시간이 짧은 솔루션



사용하기 쉬운 개발도구

### SSL 기본적으로 제공

무료로 제공해줌

### 롤백

버튼 한 번으로 이전 버전으로 돌릴 수 있음, 이는 큰 장점!



### 



### A/B 테스트

서비스로 유입된 사용자를 반으로 나눠서 만든 기능을 테스트함

최신 기능을 업데이트한 다음에 일부 사용자에게는 최신 기능을 보여줌, 

전체 다 적용하면 무슨 문제가 생길 줄 모르므로 비율을 나눠서 적용함, 분석 좋아하는 사람들은 A/B 테스트 기능을 많이 사용함 

### Analytics

1억건이면 7천만원... 회사에서 구매할 수가 없어서 걷어낸 적이 있다. 

다만 개인이 사용하기에는 좋을 수도..!



### 호스팅

저장된 크기는 1GB, 전송은 10GB까지 가능

### API는 부하를 줄여야 한다.

API는 정말 데이터만 준다. S3같은 하드디스크 서버에 이미지를 올려놓는다.여기에는 중요한 정보는 안 올린다.

이와 관련된 서버가 스토리지이다. 

### 단점은 크롤링은 안됨, 외부사이트로 나가는 건 막아놓음



### API

API는 외부에 있는데 Remote config로 외부에 서버를 받아오는 작업을 했었다.

실제 업무에서는 많이 안 쓰이는 부분이 있다. 제약사항도 있고..!



```bash
npm install firebase-tools --global
firebase login
firebase init
npm run build
firebase serve
```

### 기존 파일을 조금이라도 수정했다면 build를 새롭게 계속해야 한다. 

수정 이후 빌드를 하고 서버를 올려서 시작한다.!

```bash
npm run build
```

### Deploy complete! 배포

```bash
firebase deploy
```

[내가 만든 Todo 앱](https://vuejs-5c462.firebaseapp.com/)

## Firestore 

### Firestore 란 무엇인가?

글로벌 앱을 위해 구축된 NoSQL 데이터베이스

원하는 대로 데이터 쿼리 및 구조화

진정한 서버리스 앱 개발

기기 간, 온라인/오프라인 데이터 동기화

강력한 사용자 기반 보안

## Vue To Do App Firestore 연동

```bash
npm install vue-firestore --save
```



### firestore()

```javascript
firestore() {
  return {
    // todoItems: this.firestore.collection('todos')
    todoItems: this.firestore.collection('todos').orderBy("date")
    // todoItems: this.firestore.collection('todos').orderBy("date", "desc")
  }
},
```



### Firebase add Todo

```javascript
addTodo(value) {
  this.firestore.collection('todos').add({
    todo: value
  })
},
```

```javascript
addTodo(value) {
	const timestamp = new Date().getTime()
  this.firestore.collection('todos').add({
    todo: value,
    date: timestamp,
    createAt: new Date, // 보통 이런 식으로 변수명과 값을 넣기도 한다.
  })
},
```



### Firebase removeTodo

빼는 순간 데이터가 바로 갱신이 된다. 그래서 splice같은 코드가 필요 없다.

```javascript
removeTodo(key, index) {
  this.firestore.collection('todos').doc(key['.key']).delete()
  // 빼는 순간 데이터가 바로 갱신이 된다. 
  // 그래서 splice같은 코드가 필요 없다. 
},
```

### Firebase RemoveAll

```javascript
removeAll() {
	// get으로 전체를 가져옴
	// 그리고 비동기로 돔
	this.firestore.collection('todos').get().then(todos => {
		todos.forEach(todo => {
			todo.ref.delete()
		})
	})
},
```


