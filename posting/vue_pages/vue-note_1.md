---
title: "Vue.js란?"
permalink: /vue/
author_profile: true
toc: true
toc_label: "Vue목차"
toc_icon: "cog"
toc_sticky: true
---

## `목차`

[1. MVVM 모델에서의 Vue](###1-mvvm-모델에서의-vue)

[2. 기존 웹 개발 방식](###2-기존-웹-개발-방식)

[3. Reactivity 구현 (반응성)](###3-reactivity-구현-반응성)

[4. Reactivity 코드 라이브러리화 하기](###4.-reactivity-코드-라이브러리화-하기)

[5. Hello Vue.js와 뷰 개발자 도구](###5.-hello-vue.js와-뷰-개발자-도구)

<br>

---

<br/>

### 1. MVVM 모델에서의 Vue

<br/>

<!-- vue1.png -->

![이미지](/posting/vue_pages/notes_img/vue1.png)

<br/>

---

<br/>

### 2. 기존 웹 개발 방식

<br/>

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

<br/>

---

<br/>

### 3. Reactivity 구현 (반응성)

<br/>

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
Object.defineProperty(viewModel, "str", {
  get: function () {
    console.log("접근");
  },
  set: function (newValue) {
    console.log("할당", newValue);
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

<br>

---

<br>

### 4. Reactivity 코드 라이브러리화 하기

<br>

코드

```js
(function () {
  function init() {
    Object.defineProperty(viewModel, "str", {
      get: function () {
        console.log("접근");
      },
      set: function (newValue) {
        console.log("할당", newValue);
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

<br>

---

<br>

### 5. Hello Vue.js와 뷰 개발자 도구

<br>
Vue 스크립트 소스

```html
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```
