---
title: 'Vue.js 시작하기'
permalink: /vue/
type: pages
sidebar:
  nav: 'vueside'
toc: true
toc_label: 'Vue.js 시작하기'
---

# 섹션 1. Vue.js 소개

---

## 1. MVVM 모델에서의 Vue

![vue_1-1](/posting/vue_pages/notes_img/vue_1-1.png)

---

## 2. 기존 웹 개발 방식


HTML, CSS, JavaScript 를 따로따로 작성해서 웹 구현

```javascript
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <div id="app"></div>

    <scrip>
      // console.log(div);
      var div = document.querySelector('#app');
      var str = 'hello world';
      div.innerHTML = str;
      str = 'hello world!!!';
      div.innerHTML = str;
    </scrip>
  </body>
</html>
```

---

## 3. Reactivity 구현 (반응성)

`Reactivity` 란 데이터의 변화를 라이브러리에서 감지해서 알아서 화면을 자동으로 그려주는것.

```js
Object.defineProperty(대상 객체, '객체의 속성', {
            //정의할 내용

  //속성에 접근했을 때의 동작을 정의
  get:function(){
  },

  //속성의 값을 할당했을 때의 동작을 정의
  set: function(){
  },
})
```

Object.defineProperty()

<br>

```js
Object.defineProperty(viewModel, 'str', {
  get: function () {
    console.log('접근');
  },
  set: function (newValue) {
    console.log('할당', newValue);
    div.innerHTML = newValue;
  },
});
```

콘솔에서 viewModel.str을 치면  
'접근' 이 출력되고

콘솔에서 viewModel.str = "값" 을 바꾸면  
'할당', newValue(받은값) 이 출력되고  
div.innerHTML에 newValue 가 출력된다.
(데이터가 바인딩되어 브라우저창에 값이 출력되었다 )

(데이터 바인딩: 함수를 호출할때 그 해당 함수가 위치한 메모리 주소로 연결해주는것을 의미)

---

## 4. Reactivity 코드 라이브러리화 하기

코드

```js
(function () {
  function init() {
    Object.defineProperty(viewModel, 'str', {
      get: function () {
        console.log('접근');
      },
      set: function (newValue) {
        console.log('할당', newValue);
        render(newValue);
      },
    });
  }
  function render(value) {
    div.innerHTML = value;
  }
  init();
})();
```

<br>

구조

```javascript
{
  전체함수;
  {
    함수init;
    {
      속성정의함수;
      {
        함수get;
        console.log(출력);
      }
      {
        함수set(값);
        console.log(출력, 값);
        전달함수(값);
      }
    }
  }
  {
    전달함수(받은값);
    innerHTML = 받은값;
  }
  {
    init;
  }
}
```

<br>

진행순서:

```md
전체함수 -> 함수init -> 속성정의함수 ->  
함수get ->출력 ->  
함수set -> 출력 -> 안쪽전달함수 ->  
밖전달함수 -> innerHTML=받은값 출력
```

---

## 5. Hello Vue.js와 뷰 개발자 도구

Vue 스크립트 소스

```html
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```

---

# 섹션 2. 인스턴스

---

## 1. 인스턴스 소개

* 인스턴스는 뷰로 개발할 때 필수로 생성해야 하는 코드

* 모든 Vue 앱은 Vue 함수로 새 Vue 인스턴스를 만드는 것부터 시작한다.

<br>

_인스턴스 생성 방법_

1. body 안에 script src 와 script 태그를 붙여준다
2. `el` 에 HTML element를 쓴다
3. 그 외 속성과 api를 쓴다.

```html
<body>
  <div id="app"></div>
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <script>
    var vm = new Vue({
      el: '#app',
      data: {
        message: 'hi',
      },
    });
  </script>
</body>
```

---

## 2. 인스턴스와 생성자 함수

**생성자 함수** : _재사용할 수 있는 객체 생성 코드를 구현하는 것._

- 함수 이름의 첫 글자는 대문자로 시작합니다.

- 반드시 "new" 연산자를 붙여 실행합니다.

<br>

크롬 콘솔창에서 생성자 함수를 만든 모습.

```js
> function Person(name, job){
  //this = {}; 빈 객체가 암시적으로 만들어짐
      this.name = name;
      this.job = job;
  //새로운 프로퍼티를 this에 추가함.
  }
  //this가 암시적으로 반환됨.
< undefined
  ---------------------------
> var p = new Person ('josh', 'developer')
  // p라는것을 Person 함수를 이용해 만들고 this의 속성안에 값을 넣어 정의해줌.
< undefined
  ---------------------------
> p
  //p를 실행

< Person {name: "josh", job: "developer"}
  job: "developer"
  name: "josh"
  __proto__: Object
  // p의 속성이 정의된것을 볼수있다.
  ---------------------------
```

---

## 3. 인스턴스 옵션 속성

인스턴스의 속성, API들

```js
new Vue({
  el: ,
  template: ,
  data: ,
  methods: ,
  created: ,
  watch: ,
  router: ,
  components:{
    template
    props
    method
  },
});
```

el : _인스턴스가 그려지는 화면의 시작점 (특정 HTML 태그)_

template : _화면에 표시할 요소 (HTML, CSS 등)_

data : _뷰의 반응성(Reactivity)이 반영된 데이터 속성_

methods : _화면의 동작과 이벤트 로직을 제어하는 메서드_

created : _뷰의 라이프 사이클과 관련된 속성_

watch : _data에서 정의한 속성이 변화했을 때 추가 동작을 수행할 수 있게 정의하는 속성_

---

# 섹션 3. 컴포넌트

---

## 1. 컴포넌트 소개

`컴포넌트`는 화면의 영역을 구분하여 개발할 수 있는 뷰의 기능이다.

컴포넌트 기반으로 화면을 개발하게 되면 코드의 __재사용성__ 이 올라가고 빠르게 화면을 제작할 수 있다.

![vue_3-1](/posting/vue_pages/notes_img/vue_3-1.png)

---

## 2. 컴포넌트 등록 및 실습

```html
  <body>
    <div id="app">
      <app-header></app-header>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
  // Vue.component('컴포넌트 이름', 컴포넌트 내용);
      Vue.component('app-header', {
        template: '<h1>Header</h1>',
      });
// Vue 생성, ele 선택
      new Vue({
        el: '#app',
      });
    </script>
  </body>
```

1. new Vue를 만들어 el: '#app'을 잡는다.
2. Vue.component라는 메소드로 'app-header'란 이름을 준다
3. 컴포넌트 내용에 template속성을 이용해 \<h1>Header\</h1>를 넣었다.
__정리__: Vue 로 el #app을 선택후 컴포넌트로 이름과 속성을 주고 선택한 #app태그 안쪽에 이름'app-header'를 넣으면 속성이 실행된다.

---

## 3. 전역 컴포넌트 등록

```html
  <body>
    <div id="app">
      <app-header></app-header>
      <app-content></app-content>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
  // (Vue.componet = 전역컴포넌트)
      Vue.component('app-header', {
        template: '<h1>Header</h1>',
      });

      Vue.component('app-content', {
        template: '<h2>content</h2>',
      });

      new Vue({
        el: '#app',
      });
    </script>
  </body>
```

---

## 4. 지역컴포넌트

```html
  <body>
    <div id="app">
      <app-header></app-header>
      <app-content></app-content>
      <app-footer></app-footer>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>

      // (Vue.componet = 전역컴포넌트)
      Vue.component('app-header', {
        template: '<h1>Header</h1>',
      });
      Vue.component('app-content', {
        template: '<h2>content</h2>',
      });

      new Vue({
        el: '#app',
        //지역 컴포넌트 등록방식
        components: {
          // '컴포넌트 이름(key)': {컴포넌트 내용(value)}
          'app-footer': {
            template: '<footer>footer</footer>',
          },
        },
      });
    </script>
  </body>
</html>
```

---

## 5. 전역 컴포넌트와 지역 컴포넌트의 차이점

* 지역 컴포넌츠는 복수이기때문에 s가 붙어서 components라고 한다.  

* 일반적으로 지역 컴포넌츠로 등록해나가면서 사용을 하며 전역컴포넌트는 라이브러리나 전역으로 세팅할때 사용한다.

---

## 6. 컴포넌트와 인스턴스와의 관계

지역컴포넌트를 등록안한 지역에 사용하면 작동하지 않으며 일반적으로 실무에서는 전역컴포넌트보다는 지역컴포넌트를 사용한다.  
즉, 인스턴스 하나를 붙이고 그안에 컴포넌트 붙여나가는 방식으로 진행한다.

---

# 섹션 4. 컴포넌트 통신 방법 - 기본

---

## 1. 컴포넌트 통신

![vue_4-1](/posting/vue_pages/notes_img/vue_4-1.png)

---

## 2. 컴포넌트 통신 규칙이 필요한 이유

데이터의 흐름을 추적하기 어려운 문제점을 해결하기 위하여 event 를 올려보내고 props를 내려보내는 방식의 규칙으로 사용한다.

![vue_4-2](/posting/vue_pages/notes_img/vue_4-2.png)

---

## 3. props 속성

- __props__: property의 약자로 부모에게 받아온 데이터.

<br>

```html
<app-header v-bind:프롭스 속성이름="상위 컴포넌트 데이터 이름"></app-header>
```

의 문법을 사용하여 components안에 가져오고싶은 data를 가져올수있다.

---

## 4. props 속성의 특징

정리:
1. Vue를 생성후 el: '#app' 지역에 사용하겟다고 말한다  

2. components: 와 data: 를 만든다.
   * components의 이름을 app-header라짓고 안에 template과 props의 속성을 줫다.
   * data에는 message에 속성을 줫다.  

3. 그후 app-header(컴포넌트)에 만들어놓은 data를 가져다 썻다. 

```html
    <app-header v-bind:propsdata="message"></app-header> 
```

```html
  <body>
    <div id="app">
      <!-- <app-header v-bind:프롭스 속성이름="상위 컴포넌트 데이터 이름"></app-header> -->
      <app-header v-bind:propsdata="message"></app-header>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
      var appHeader = {
        template: '<h1>header<h1>',
        props: ['propsdata'],
      };

      new Vue({
        el: '#app',
        components: {
          'app-header': appHeader,

        },
        data: {
          message: 'hi',
        },
      });
    </script>
  </body>
```

---

## 5. props 속성 실습

```html
  <body>
    <div id="app">
      <app-header v-bind:propsdata1="message"></app-header>
      <app-content v-bind:propsdata2="num"></app-content>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>

      var appHeader = {
        template: '<h1>{{ propsdata1 }}</h1>',
        props: ['propsdata1'],
      };

      var appContent = {
        template: '<div>{{propsdata2}}</div>',
        props: ['propsdata2']
      };

      new Vue({
        el: '#app',

        components: {
          'app-header': appHeader,
          'app-content': appContent,
        },
        
        data: {
          message: 'hi',
          num: 10,
        },
      });

    </script>
  </body>
```

크롬 Vue창과 화면창에  
propsdata1: hi  
propsdata2: 10  
이 나온다.

---

## 6. event emit

* event 올라가는 구조: ([컴포넌트 통신 방식](#2.-컴포넌트-통신-규칙이-필요한-이유) 참조)

<br>

```html
  <body>
    <div id="app">
      <app-header> </app-header>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

    <script>
      var appHeader = {
        template: '<button v-on:click="passEvent">click me</button>',
        methods: {
          passEvent: function () {
            this.$emit('pass');
          },
        },
      };

      new Vue({
        el: '#app',
        components: {
          'app-header': appHeader,
        },
      });
    </script>
  </body>
```

1. methods에 passEvent를 정의했다.
2. template에 버튼을 만들고 v-on:click="____"을 준다음 passEvent 함수를 넣어줫다.
3. this.$emit() 라는 Vue.js에서 제공하는 api(기능)을 이용하여 'pass'라는 값을 넣어줫다.

---

## 7. event emit으로 콘솔 출력하기

![vue_4-7](/posting/vue_pages/notes_img/vue_4-7.png)

* 상위에서 하위로는 데이터를 내려줌, 프롭스 속성
* 하위에서 상위로는 이벤트를 올려줌, 이벤트 발생

---

## 8. event emit 실습

```html
 <body>
    <div id="app">
      <p>{{num}}</p>
      <app-header v-on:decrease="decreaseNumber"> </app-header>
      <app-content v-on:increase="increaseNumber"> </app-content>

    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
    //하위컴포넌트(appHeader)
      var appHeader = {
        template: '<button v-on:click="deleteNumber">minus</button>',
        methods: {
          deleteNumber: function () {
            this.$emit('decrease');
          },
        },
      };
    // 하위컴포넌트(appContent)
      var appContent = {
        template: '<button v-on:click="addNumber">plus</button>',
        methods: {
          addNumber: function () {
            this.$emit('increase');
          },
        },
      };
    //상위 컴포넌트(root)
      new Vue({
        el: '#app',
        components: {
          'app-header': appHeader,
          'app-content': appContent,
        },
        methods: {
          decreaseNumber: function () {
            this.num = this.num - 1;
          },
          increaseNumber: function () {
            this.num = this.num + 1;
          },
        },
        data: {
          num: 10,
        },
      });
    </script>
  </body>
```

---

## 9. 인스턴스에스의 this

this 는 해당 object를 가리키며 
this의 속성이름을 사용해서 해당위치나 값을 구한다.  

```js
var vm = new Vue({
  el: '#app',
  components: {
    'app-header': appHeader,
    'app-content': appContent,
  },
  methods: {
    decreaseNumber: function () {
      this.num = this.num - 1;
    },
    increaseNumber: function () {
      this.num = this.num + 1;
    },
  },
  data: {
    num: 10,
  },
});
```

__ex)__

* this는 vm을 가리킨다.  
* this.num = 10 이다

---

# 섹션 5. 컴포넌트 통신 방법 - 응용

---

## 1. 같은 컴포넌트 레벨 간의 통신 방법

```html
  <body>
    <div id="app">
      <app-header v-bind:propsdata="num"></app-header>
      <app-content v-on:pass="deliverNum"></app-content>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
      const appHeader = {
        template: '<div>header</div>',
        props: ['propsdata'],
      };
      const appContent = {
        template:
          '<div>content<button v-on:click="passNum">pass</button></div>',
        methods: {
          passNum: function () {
            this.$emit('pass', 10);
          },
        },
      };

      new Vue({
        el: '#app',
        components: {
          'app-header': appHeader,
          'app-content': appContent,
        },
        data: {
          num: 0,
        },
        methods: {
          deliverNum: function (value) {
            this.num = value;
          },
        },
      });
    </script>
  </body>
```

\- __event를 root컴포넌트에 올리기__ -

1. appContent에서 버튼을 만들고 v-on으로 클릭하면 passNum이 실행되게 만든다.  

2. passNum이 되면this.$emit('pass',10)을 한다.  

3. app-content에서 10을 pass로 받고 root의 method에 있는 deliverNum에 넘겨준다.  

4. root에 기본 data값을 num:0으로 주고 deliverNum에서 값을 받으면 그 값이 num이 되도록 this.num = value 를 준다.  


\- __root컴포넌트의 num값을 props로 내리기__ -

1. appHeader를 만든후 props를 만든다.  

2. app-header에서 v-bind:propsdata="num"이라 정의한다. 즉, 상위 root에 있는 num의 값을 하위 컴포넌트인 appHeader의 propsdata로 가져온다.  

__** `요약` **__

1. 하위 appContent에서 method-passNum-this.$emit으로 10을 상위로 root-method를 통해 data에 전달했다  

2. 상위 root의 num 값을 하위 appHeader의 propsdata로 app-header를 통해 전달했다.

---

# 섹션 6. 라우터

---

## 1. 뷰 라우터 소개와 설치

설치법

1. https://router.vuejs.org/installation.html#direct-download-cdn 를 접속.

2. CDN 복사 
   https://unpkg.com/vue-router/dist/vue-router.js

3. script scr에 붙여넣기.

---

## 2. 뷰 라우터 인스턴스 연결 및 초기 상태 안내

(참고1)

```html
<body>
   <div id="app">
   </div>
   <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
   <script src="https://unpkg.com/vue-router/dist/vue-router.js"></script>
   <script>
     const router = new VueRouter({
     });
     new Vue({
       el: '#app',
       router: router,
     });
   </script>
 </body>
```

(참고2)

```html
<body>
  <div id="app"></div>
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <script src="https://unpkg.com/vue-router/dist/vue-router.js"></script>
  <script>
    const LoginComponent = {
      template: '<div>login</div>',
    };
    const MainComponent = {
      template: '<div>main</div>',
    };
    const router = new VueRouter({
      //페이지의 라우팅 정보
      routes: [
        {
          // 페이지의 url
          path: '/login',
          // 해당 url에서 표시될 컴포넌트
          componenet: LoginComponent,
        },
        {
          path: '/main',
          component: MainComponent,
        },
      ],
    });
    new Vue({
      el: '#app',
      router: router,
    });
  </script>
</body>
```

위와 같이 라우터를 등록하고 나면 그 다음에 할 일은 라우터에 옵션을 정의하는 일이다. 대부분의 SPA 앱에서는 아래와 같이 2개 옵션을 필수로 지정한다.

routes : 라우팅 할 URL과 컴포넌트 값 지정  
mode : URL의 해쉬 값 제거 속성(hitstory를 쓰면 url에 #이  안붙는다.)  

```js
new VueRouter({
  mode: 'history',
  routes: [
    { path: '/login', component: LoginComponent },
    { path: '/home', component: HomeComponent }
  ]
})
```

---

## 3. 라우터가 표시되는 영역 및 router-view 태그 설명

```html
<div id="app">
  <router-view></router-view>
</div>
```

router-view 태그를 사용하면 라우터의 routes -> path의 url로 이동했을때 해당되는 component가 실행된다.

---

## 4. 링크를 이용한 페이지 이동 및 router-link 태그 설명

```html
<div id="app">
  <div>
    <router-link to="/login">Login</router-link>
    <router-link to="/main">Main</router-link>
  </div>
```

라우터링크는 말 그대로 링크를 제공해주는 역활을 한다. 
라우터 루트로 경로를 연결하고 컴포넌트로 template를 꾸민후 router-view로 html에 표현하고 링크를 만든다.

---

# 섹션 7. HTTP 통신 라이브러러 - axios

---

## 1. HTTP 라이브러리와 Ajax 그리고 Vue Resource

 axios는 ajax 등의 웹 통신 기능을 제공하는 라이브러리 중 하나이며 뷰에서 권고하는 HTTP 통신 라이브러리이다.

(설치법)

```html
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>

```

---

## 2. axios 소개 및 오픈 소스를 사용하기 전에 알아야 할 것들

[자바스크립트 비동기 처리와 콜백 함수](https://joshua1988.github.io/web-development/javascript/javascript-asynchronous-operation/)


[자바스크립트 Promise 이해하기](https://joshua1988.github.io/web-development/javascript/promise-for-beginners/)

[자바스크립트 async와 await](https://joshua1988.github.io/web-development/javascript/js-async-await/)

---

## 3. axios 실습 및 this 설명

```html
<body>
  <div id="app">
    <button v-on:click="getData">get user</button>
    <div>{{users}}</div>
  </div>
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
  <script>
    new Vue({
      el: '#app',
      data: {
        users: [],
      },
      methods: {
        getData: function () {
          const vm = this;
          axios
            .get('https://jsonplaceholder.typicode.com/users/')
            .then(function (response) {
              vm.users = response.data;
            })
            .catch(function (error) {
              console.log(error);
            });
        },
      },
    });
  </script>
</body>
```

  1. 버튼을 만들고 클릭하면 getData 호출
  2. methods의getData가 실행됨.
  3. axios.get(주소) 가 실행됨
  4. 실패시catch한다 (console.log(error)실행)
  5. 성공시 .then의 function()을 실행
  6. vm= this 라고 해놧기때문에 vm.users = response.data 가 가능하다.
  7. {{users}}로 화면에 가져온 users, 즉 response.data를 뿌림.

---

## 4. 웹 서비스에서의 클라이언트와 서버와의 HTTP 통신 구조

![vue_7-4](/posting/vue_pages/notes_img/vue_7-4.png)

---

## 5. 크롬 개발자 도구 네트워크 패널 보는 방법

chrome 개발자도구 -> 네트워크패널 -> xhr 필터(선택) -> Name에서 파일클릭 -> Headers칸에서 Response Headers와 Request Headers, General 등을 볼 수 있고 Preview에서 배열로 된 정보를 볼수 있다.

---

# 섹션 8. 템플릿 문법 - 기본

---

## 1. 템플릿 문법 소개

---

### 1. 데이터 바인딩

데이터 바인딩은 뷰 인스턴스에서 정의한 속성들을 화면에 표시하는 방법이다. 콧수염 괄호(Mustache Tag)라고 한다.

```html
<div>{{ message }}</div>
```

```js
new Vue({
  data: {
    message: 'Hello Vue.js'
  }
})
```

### 2. 디렉티브

디렉티브는 뷰로 화면의 요소를 더 쉽게 조작하기 위한 문법이다. 화면 조작에서 자주 사용되는 방식들을 모아 디렉티브 형태로 제공하고 있다. 예를 들어 아래와 같이 특정 속성 값에 따라 화면의 영역을 표시하거나 표시하지 않을 수 있음


```html
<div>
  Hello <span v-if="show">Vue.js</span>
</div>
```

```js
new Vue({
  data: {
    show: false
  }
})
```

**자주 사용되는 디렉티브**

* v-bind
* v-on
* v-model

---

## 2. 데이터 바인딩과 computed 속성

computed: 계산된 속성

```html
<body>
  <div id="app">
    <p>{{num}}</p>
    <p>{{doubleNum}}</p>
  </div>

  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <script>
    new Vue({
      el: '#app',
      data: {
        num: 10,
      },
      computed: {
        doubleNum: function () {
          return this.num * 2;
        },
      },
    });
  </script>
</body>
```

data에 num을 10을 준후 computed라는 속성으로 doubleNum을 만들고 함수를 사용해 return this.num*2를 해 주었다. 그 후 데이터 바인딩으로 화면 출력.

---

## 3. 뷰 디렉티브와 v-bind

```html
<body>
  <div id="app">
    <p v-bind:id="uuid" v-bind:class="name">{{num}}</p>
    <!-- <p id="abc1234" class="text-blue">{{num}}</p> (연결되었을때 잡힐 id와 class) -->
    <p>{{doubleNum}}</p>
  </div>
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <script>
    new Vue({
      el: '#app',
      data: {
        num: 10,
        uuid: 'abc1234',
        name: 'text-blue',
      },
      computed: {
        doubleNum: function () {
          return this.num * 2;
        },
      },
    });
  </script>
</body>
```

이전 예시에서 uuid를 data에 추가한 후 v-bind로 연결해서 p태그의 id 값이 uuid의 값이 되도록 만들었다.  

똑같은 방식으로 data에 name을 만들고 v-bind로 class도 연결해 주었다.

---

## 4. 클래스 바인딩, v-if, v-show

```html
<body>
  <div id="app">
    <div v-if="loading">Loading...</div>
    <div v-else>test user has been logged in</div>
    
    <div v-show="loading">Loading...</div>
  </div>

  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <script>
    new Vue({
      el: '#app',
      data: {
        loading: true,
      },
    });
  </script>
</body>
```

data에 loading을 boolean으로 주고 v-if/else 와 v-show 두가지 방법으로 화면에 나타내어 봣다.
v-if/else 는 false일시 else만 나타나고 true값은 없는 반면 v-show는 false 일때 CSS의 display만
none으로 바꿔주는 차이가 있다.

---

## 5. 모르는 문법이 나왔을 때 공식 문서를 보고 해결하는 방법

data안에 message:''을 준 후,

```html
      <input v-model="message" placeholder="edit me" />
      <p>{{ message }}</p>
      <!-- todo: 인풋 박스를 만들고 입력된 값을 p 태그에 출력해보시오 -->
```

를 하면 화면에 인풋창에 입력하는것이 밑 p태그에 출력된다.

__모르는 문법이 나왔을시 Vue 공식 홈페이지 [https://vuejs.org](https://vuejs.org/) 에서 검색 하여 해결한다.__  

위 예시는 input창을 쓰니까 공식홈페이지에서 _input_ 을 검색했다.

---

## 6. method 속성과 v-on 디렉티브를 이용한 키보드, 마우스 이벤트 처리 방법

v-on은 keyboard, mouse 등의 입력을 받을 수 있는 디렉티브
.enter는 해당 디렉티브 이벤트에 대한 modifier(수식어).

아래의 v-on:keyup.enter은 키보드를 친후 엔터를 눌렀을때를 말한다.

```html
<body>
  <div id="app">
    <button v-on:click="logText">Click Me</button>
    <input type="text" v-on:keyup.enter="logText" />
  </div>
  
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"><script>
  <script>
    new Vue({
      el: '#app',
      methods: {
        logText: function () {
          console.log('clicked');
        },
      },
      data: {},
    });
  </script>
</body>
```

---

# 섹션 9. 템플릿 문법 -실전

---

## 1. watch 속성

















---

## 2. watch 속성 vs computed 속성

---

## 3. computed 속성을 이용한 클래스 코드 작성 방법

---

# 섹션 10. 프로젝트 생성 도구 - Vue CLI

---

## 1. 최신 Vue CLI 소개

---

## 2. Vue CLI 도구 설치할 때 문제점 해결 방법

---

## 3. CLI 2.x와 3.x의 차이점 / 프로젝트 생성 및 서버 실행

---

## 4. CLI로 생성한 프로젝트 폴더 구조 확인 및 main.js 파일 설명

---

## 5. 싱글 파일 컴포넌트 소개 및 여태까지 배운 내용 적용하는 방법

---

## 6. App.vue와 HelloWorld.vue 설명

---

# 섹션 11. 싱글 파일 컴포넌트

---

## 1. 싱글 파일 컴포넌트에 배운 내용 적용하여 개발 시작하기

---

## 2. 싱글 파일 컴포넌트 체계에서 컴포넌트 등록하기

---

## 3. 싱글 파일 컴포넌트에서 props 속성 사용하는 방법

---

## 4. 싱글 파일 컴포넌트에서 event emit 구현하기

---

## 5. Vue CLI로 생성한 프로젝트 내용 정리

---

# 섹션 12. 최종 프로젝트 - 사용자 입력 폼 만들기

---

## 1. 프로젝트 생성 및 마크업 작업

---

## 2. v-model 속성과 submit 이벤트 처리

---

## 3. axios를 이용한 데이터 전송 및 form 구현

---

# 섹션 13. 마무리

---

## 1. 수업 정리 및 향후 학습 방향 안내