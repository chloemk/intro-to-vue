# Intro to Vue.js

---

## Reactivity

Vue.js의 추구하는 중심사상이자 핵심 기능입니다.
데이터에 대한 변화를 뷰에서 감지해서 화면에 반영하는 것부터 화면 조작에 대한 api라던지 속성들을 뷰에서 제공합니다.

> [What is Vue.js](https://github.com/chloemk/intro-to-vue/blob/main/notes/What%20is%20Vue.js.md 'Note #1')

---

## 인스턴스

뷰로 개발할때 필수로 생성해야하는 단위입니다. 인스턴스 안에 어떤 내용들을 추가함으로써 화면을 조작할 수 있습니다.

> [Instance](https://github.com/chloemk/intro-to-vue/blob/main/notes/Instance.md 'Note #2')

---

## 컴포넌트

화면의 영역을 구분해서 개발하는 방식입니다.
`코드의 반복을 최대한 줄일 수 있다. (재사용성 높음)`

> [Components](https://github.com/chloemk/intro-to-vue/blob/main/notes/Component.md 'Note #3')

---

## 컴포넌트 통신

컴포넌트로 개발할 때 데이터의 흐름을 제어하기 위한 데이터의 규칙들을 제한하면서 제안했을 때 이점들이 있습니다.
여러명에서 같이 개발하더라도 서로 같이 데이터에 대한 흐름을 예측할 수 있습니다.

- props (상위 -> 하위)
- event emit (하위 -> 상위로 이벤트로 올림)

> [Components2](https://github.com/chloemk/intro-to-vue/blob/main/notes/Component2.md 'Note #4')

---

## 라우터

Vue에서는 VueRouter라는 공식 라이브러리를 통해 라우터 기능을 지원합니다.
VueRouter 인스턴스를 생성하여 라우터 옵션을 지정한 후 Vue 인스턴스에 라우터를 등록하여 사용합니다.

- router-view : 변경되는 url에 따라 컴포넌트를 뿌려줍니다.
- router-link : 페이지 이동을 위한 링크 태그입니다.

> [Router](https://github.com/chloemk/intro-to-vue/blob/main/notes/Router.md 'Note #5')

---

## 템플릿 문법

화면을 조작하기 위한 뷰의 문법들을 의미한다. 크게 두가지가 존재한다.

- 데이터 바인딩 (Reacitvity와 비슷한 개념. 데이터의 변화에 따라서 화면에 반영해주는 것이 reactivity이고, 실제로 데이터를 화면에 엮어내는 부분이 데이터 바인딩이다.)
- 뷰 디렉티브 (화면을 조작하기 위해서 뷰가 추가적으로 제공하는 문법. v- 이런 html속성으로 이루어져있다.)

> [Template](https://github.com/chloemk/intro-to-vue/blob/main/notes/CLI.md 'Note #6')

---

## Vue CLI

프로젝트를 생성할 때 명령어를 이용해서 생성하는 방식을 CLI라고 합니다.

> [Vue CLI](https://github.com/chloemk/intro-to-vue/blob/main/notes/CLI.md 'Note #7')

---

## 싱글 파일 컴포넌트

.vue 파일이 내부적으로 어떻게 들어가는지 궁금하면 웹팩 공식문서 참고
웹팩의 기능중에 뷰 로더가 있는데 싱글 파일 컴포넌트의 내용을 찢어서 브라우저가 이해할 수 있는 형태로 바꿔준다.
