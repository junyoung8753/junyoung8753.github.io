---
title: "인스턴스"
permalink: /vue/instance/
toc: true
---

## `목차`

[1. 인스턴스 소개](##1.-인스턴스-소개)

[2. 인스턴스와 생성자 함수](##2.-인스턴스와-생성자-함수)

[3. 인스턴스 옵션 속성](##3.-인스턴스-옵션-속성)

<br>

---

<br/>

## 1. 인스턴스 소개

<br/>

인스턴스는 뷰로 개발할 때 필수로 생성해야 하는 코드

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
      el: "#app",
      data: {
        message: "hi",
      },
    });
  </script>
</body>
```

<br>

---

<br/>

## 2. 인스턴스와 생성자 함수

<br/>

**생성자 함수** : _재사용할 수 있는 객체 생성 코드를 구현하는 것._

- 함수 이름의 첫 글자는 대문자로 시작합니다.

- 반드시 "new" 연산자를 붙여 실행합니다.

<br/>

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

<br/>

---

<br/>

## 3. 인스턴스 옵션 속성

<br/>

인스턴스의 속성, API들

```js
new Vue({
  el: ,
  template: ,
  data: ,
  methods: ,
  created: ,
  watch: ,
});
```

el : _인스턴스가 그려지는 화면의 시작점 (특정 HTML 태그)_

template : _화면에 표시할 요소 (HTML, CSS 등)_

data : _뷰의 반응성(Reactivity)이 반영된 데이터 속성_

methods : _화면의 동작과 이벤트 로직을 제어하는 메서드_

created : _뷰의 라이프 사이클과 관련된 속성_

watch : _data에서 정의한 속성이 변화했을 때 추가 동작을 수행할 수 있게 정의하는 속성_

<br/>
