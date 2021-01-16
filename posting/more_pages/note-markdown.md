---
title: "Markdown 사용법"
toc_label: "Markdown 사용법"
permalink: /more/markdown/
author_profile: true
toc_sticky: true
---

## 헤더

```markdown
    # 헤더
    ## 2단계
    ### 3단계
    #### 4단계
    ##### 5단계
    ###### 6단계
```

---

## 리스트

1.  첫번째
1.  두번째
1.  세번째

- 순서없음

* 들여쓰기1
  - 들여쓰기2
    - 들여쓰기3

.

```markdown
    1.첫번째
    2.두번째
    3.세번째
    +순서없음
      - 들여쓰기1
        * 들여쓰기2
          + 들여쓰기3
```

---

## 인용구

> 인용구1
>
> > 인용구2
> >
> > > 인용구3

```markdown
    > 인용구1
    >> 인용구2
    >>> 인용구3
```

---

## 글씨체

- <u>밑줄치기</u>
- **볼드**
- _이탈릭체_
- ~~취소선~~
- `강조`

  <u>**_ex) ~~볼드+이탈릭+취소선+밑줄+`강조`~~_**</u>

.

```markdown
    * <u>밑줄치기</u>
    * __볼드__
    * _이탈릭체_
    * ~~취소선~~
    * `강조`
    <u>___ex) ~~볼드+이탈릭+취소선+밑줄+`강조`~~___</u>
```

---

## 링크

- 유형1: [Google](https://google.com "구글로 이동")  
  구조: `[설명](URL주소 "호버링메시지 작성란")`

- 유형2: <https://google.com>  
  구조: `<URL 주소>`

- 유형3: [맨위로가기](#markdown-사용법)  
  구조: `[설명](#동일파일의 가고싶은 문단)`
  - 문단작성법  
    ex) `# Markdown 사용법! -> #markdown-사용법`
  1. 특수문자 제거
  2. 스페이스 `-` 로 변경
  3. 소문자로 변경

.

```markdown
    - 유형1: [Google](https://google.com '구글로 이동')
      구조: `[설명](URL주소 "호버링메시지 작성란")`

    - 유형2: <https://google.com>
      구조: `<URL 주소>`

    - 유형3: [맨위로가기](#markdown-사용법)
    구조: `[설명](#동일파일의 가고싶은 문단)`
      + 문단작성법
      ex) `# Markdown 사용법! -> #markdown-사용법`
      1. 특수문자 제거
      2. 스페이스 ` - ` 로 변경
      3. 소문자로 변경
```

---

## 이미지삽입

유형1: 바로 `이미지` 삽입  
구조: `![이미지이름](이미지URL` "호버링시 설명")
![이미지](https://www.dhresource.com/0x0/f2/albu/g6/M00/53/1F/rBVaR1qrJpGAShZwAAJyu2m3cZ8387.jpg/new-women-sexy-set-two-piece-suit-pure-color.jpg "사람1")

유형2: `HTML 태그`로 삽입 (사이즈조절가능)  
구조: `<img src`="" width="" height="">
<img src="https://www.dhresource.com/0x0/f2/albu/g6/M00/53/1F/rBVaR1qrJpGAShZwAAJyu2m3cZ8387.jpg/new-women-sexy-set-two-piece-suit-pure-color.jpg" width="50%" height="50%">

유형3: 이미지 삽입 후, `링크 걸기`  
구조: [유형1](링크)
[![이미지](https://www.dhresource.com/0x0/f2/albu/g6/M00/53/1F/rBVaR1qrJpGAShZwAAJyu2m3cZ8387.jpg/new-women-sexy-set-two-piece-suit-pure-color.jpg "사람1")](http://www.vidhist.com/wordpress/why-did-you-click-on-this-link/)

```markdown
    유형1: 바로 `이미지` 삽입
    구조: `![이미지이름](이미지URL` "호버링시 설명")
    ![이미지](https://www.dhresource.com/0x0/f2/albu/g6/M00/53/1F/    rBVaR1qrJpGAShZwAAJyu2m3cZ8387.jpg/    new-women-sexy-set-two-piece-suit-pure-color.jpg '사람1')

    유형2: `HTML 태그`로 삽입 (사이즈조절가능)
    구조: `<img src`="" width="" height="">
    <img src="https://www.dhresource.com/0x0/f2/albu/g6/M00/53/1F/    rBVaR1qrJpGAShZwAAJyu2m3cZ8387.jpg/    new-women-sexy-set-two-piece-suit-pure-color.jpg" width="50%"   height="50%">

    유형3: 이미지 삽입 후, `링크 걸기`
    구조: [유형1](링크)
    [![이미지](https://www.dhresource.com/0x0/f2/albu/g6/M00/53/1F/   rBVaR1qrJpGAShZwAAJyu2m3cZ8387.jpg/    new-women-sexy-set-two-piece-suit-pure-color.jpg '사람1')](http://www.    vidhist.com/wordpress/why-did-you-click-on-this-link/)
```

---

## 표그리기

> _\* 예시 1_
> | 일 | 월 | 화 | 수 | 목 | 금 | 토 |
> | --- | --- | --- | --- | --- | --- | --- |
> | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
> | 8 | 9 | 10 | 11 | 12 | 13 | 14 |
> | 15 | 16 | 17 | 18 | 19 | 20 | 21 |
> |

.

> _\* 예시 2_  
> ||수학|평가 |
> :-|:-:|:-:|
> 철수| 90|참잘했어요|
> 영희|50|분발하세요|
> |

```markdown
     _\* 예시 1_
     | 일 | 월 | 화 | 수 | 목 | 금 | 토 |
     | --- | --- | --- | --- | --- | --- | --- |
     | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
     | 8 | 9 | 10 | 11 | 12 | 13 | 14 |
     | 15 | 16 | 17 | 18 | 19 | 20 | 21 |
     |

     _\* 예시 2_
     ||수학|평가 |
     :-|:-:|:-:|
     철수| 90|참잘했어요|
     영희|50|분발하세요|
     |
```

---

## 수식

일단생략

---

## 코드 블록

js, bash, cpp, dockerfile, markdown, yml, html, http, json, r, ruby, xml, sql … 등

\```javascript

\```  
적당한 언어를 쓴후 내용물을 안쪽에 넣으면 된다.

**JavaScript**

```javascript
console.log("hello world");
```

**HTML**

```html
<html>
  <head></head>
  <body></body>
</html>
```

**Markdown**

````markdown
    ### JavaScript

    ```javascript
    console.log('hello world');
    ```

    ### HTML

    ```html
    <html>
      <head></head>
      <body></body>
    </html>
    ```
````

---

## 기타

- 기능용도로 사용하는 특수문자(\*,+,- 등)를 있는 그대로 표현하고 싶은경우 **`\`** 기호를 앞에 붙이면 된다.

- 마크다운에서 지원하지 않거나 표현하기 어려운 경우 `HTML 태그`로 직접 표현하는 것도 한가지 방법이다.
  - \<br/>
  - \<img src="">
  - 등등....
