### 브라우저에 요청을 하면 과정이 어떻게 되는가?

서버에 요청을 보내면 데이터를 뿌려준다. 

### 제플린 보여주세요 

### 날씨 만드는 실습예제 pdf자료 요청하기

### 프로젝트를 위한 깃허브 레포지토리 생성하는 법

- 어떤 레포지토리를 생성해야 할까
- 프로젝트
- 팀 계정으로 판다
- 개인 레포지토리에 콜라보레이터를 준다.



# API 생성

4가지 API를 만들어야 한다.



### API 문서를 받았을 때 프론트 개발자가 미리 할 일

프론트엔드 개발자는 백엔드 개발자로부터 API문서를 받으면 내가 필요한 정보가 있는지 체크해야 한다. 만약 나중에 서버 개발 다됐는데, 무언가가 필요하다고 하면 난감함..! 그래서 미리 체크해야 한다.



## 장고 URL에 요청을 보내면

url에 입력을 하게 되면 장고가 떠있을 경우

처음 작성했던 ulrs파일을 보고! todos가 정의가 되어있으면 todos는 어떤 메소드를 호출해주라고 정의를 한다. 그리고 호출해서 데이터를 JSON으로 내려준다. 

- Model 작성
- url 매핑
- View 작성
- 

### Settings.py

```python
INSTALLED_APPS = [
  'corsheaders',
  'todos',
]
MIDDLEWARE = [
	'corsheaders.middleware.CorsMiddleware',
]
CORS_ORIGIN_ALLOW_ALL = True
CORS_ALLOW_CREDENTIALS = True
```



### Model 작성

```python
from django.db import models

# Create your models here.
class Todo(models.Model):
  todo = models.CharField(max_length=1000)
  create_date = models.DateTimeField(auto_now=True)

  def __str__(self):
    return self.todo
```

### urls.py 작성

```python
from django.urls import path
from .views import *
# 목록 4개를 한 번에 가져오기 위해

urlpatterns = [
	path('todos/', todo_list, name='list'),
]
```

### View 작성

```python
from django.shortcuts import render
from .models import Todo
from django.http import JsonResponse

# Create your views here.
def todo_list(request):
  todos = Todo.objects.all(); # 리스트로 가져온다.
  todo_list = []
  for todo in todos:
    todo_list.append({"id": todo.id, "todo": todo.todo, "create": todo.create_date})
	
  return JsonResponse(todo_list, safe=False)

```



## 파이어베이스 때는 내부적으로 통신을 해줬지만

Vue를 사용할 때는 엑시오스를 직접 사용해야 한다.

모든 프로젝트를 엑시오스를 썼었음, 보기에는 리소스처럼 보일 수는 었었지만..! 

- 그리고 슬래시를 주의하기 (주소)
- 엑시오스로 받는 변수 안에 결과가 있다. 
- JSON 타입을 얘한테 다 준다..!
- todos 화면을 뿌려준다..



## Vue.js에서의 처리

```javascript
import axios from 'axios'

Vue.prototype.$http = axios // 보통 이렇게 이름을 쓴다.
```



브라우저는 내 같은 호스트로만 통신할 수 있게끔 제약사항을 걸어놓는데, 통신을 위해서는 이것을 풀어줘야 한다.



### CORS 란?

javascript 라이브러리에서 Same Origin Policy 적용 받음

프로토콜, 호스트, 포트가 같아야만 요청이 가능



우리 프로젝트는 호스트는 같지만 포트가 다름



### 번개장터 있을 때 서버 구성

디비만을, 디비에 데이터를 저장하는! 디비의 핵심적인 로직을 처리한는! 서버가 따로 있었다.



모바일 

웹사이트



프론트 중계하는 서버르 ㄹ가운데 하나 두었다.

디비를 연결하는 서버가 둘만 허용해준다.! 프론트랑, 디비만@

가운데 디비를 연결하는 서버(백엔드 서버)가 허용해주는 포트가 제한적이다.!

### 중계 구조

백엔드에서 요청을 하면 



```
 8000            8080
------  			  ------
Django					Vue.js
```







### todos는 우리가 요청한 에이피아이다!

네트워크에 나와있는

조회할 때는 get

생성할 때는 포스트..! 

api를 타서 겟이냐 포스트이냐를 나눠준다.





```
get을 제외한 나머지는 다 토큰이 필요하다.
```



삭제하는 API를 만든다. 딜리트 메소드만 받아야 한다!! 

뷰으 투두를 가져온다.





추가를 누르면 

값을 보내면서 요청을  한다. 유알엘로 받는다. 

힘슬,ㄹ 찾고 

get('key') 값을 넣는다. 

JsonReponse





검색 엔진에 바로바로 반영이 안되는 문제가 있다.

그거 + 몇몇사람들은 로직 자체가 바깥으로 보여주는 게 싫어서 

서버사이드 렌더링을 하는 개발자도 있다. 서버에서 뷰js를 사용하면 

싱글 컴포넌트 체계를 못한다..!



다른 템플릿이랑 충돌이 날 수 있으므로..! 

뷰는 바꿔주는 포인트를 만들어놓았다.

hello world로 

뷰보다 장고의 템플릿이 먼저 작동한다. 



### console.log 로 데이터가 어디까지 들어가는지 게속 확인해라

console.log을 찍어서 데이터가 어디까지 들어가는지, 기능이 어디까지 작동하는지 확인할 수 있다. 



### 빌드를 해서 JSON으로 내보내서  장고에서 가져다 쓸 수 있다

SSR을 구현해야 한다면 어떻게든 하는 경우가 있다.



### 잘하는 신입이랑 경력자

에러가 났을 때 어디서부터 찾는가

코드는 금방 개발해도 문제가 생기면 어떻게 해결해야 하는지 모른다.

문제가 생기면 그 시점부터 버튼을 계속 찍어본다..!!

SSR에서는 맞추어줘도 된다. 



### CSS가 안 먹을 때는 캐싱을 의심해볼 수 있다.





## SSR







## Webtoon

요즘은 통테이블로 관리한다고..! 요즘은 성능이 좋아서..! 괜찮다고 한다.

게시판을 통테이블로 

게시판을 통테이블로, 안에 댓글까지 한 꺼번에 관리하기도 한다.

네이버는 이렇게 하기도 한다!





