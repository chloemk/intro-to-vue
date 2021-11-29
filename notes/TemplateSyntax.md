# [6] Vue 템플릿 문법

템플릿 문법은 뷰로 화면을 조작하는 방법을 의미하고 크게 `데이터 바인딩`과 `디렉티브`로 나뉩니다.

---

# 데이터 바인딩

뷰 인스턴스에서 정의한 속성들을 화면에 표시하는 방법입니다.
`{{}}` 콧수염 괄호는 기본적인 데이터 방식입니다.

---

# 디렉티브

디렉티브는 뷰로 화면의 요소를 더 쉽게 조작하기 위해 사용하는 지시문과 같은 문법입니다. `v-` prefix가 붙는 것이 특징입니다.

## modifier

- .enter
- .prevent

---

## v-text

element의 `textContent`를 업데이트합니다.
많이 사용되지 않는 디렉티브입니다.

```js
//script
import { ref } from 'vue';
const obj = ref({
	food: 'banana',
	subject: 'react',
});

//template
<h3 v-text='obj.food'></h3>;
```

---

## v-model

<input>, <textarea>, <select>, components 등 form 입력 엘리먼트 값 또는 컴포넌트 출력의 값을 받아올 수 있습니다.
`양방향 바인딩`을 생성합니다.

```js
//script
import { ref } from 'vue';
const obj = ref({
	food: 'banana',
	subject: 'react',
});

//template
<h2>{{ obj.subject }} 과목을 좋아해요!</h2>
<input type="text" v-model="obj.subject" />
```

---

## v-html

태그 자체를 받아와서 보여주고 싶은 경우에 사용합니다. (일반 HTML로 삽입되고, vue 템플릿으로 컴파일 되지 않습니다.)

```js
//script
const alertMessage = '<h2>경고!!</h2>';

//template
<div v-html='alertMessage'></div>;
```

웹 사이트에서 임의의 HTML을 동적으로 렌더링하면 `XSS 공격`에 취약하기 때문에 신뢰할 수 있는 경우에만 사용해야합니다. 특히 사용자가 제공한 컨텐츠에는 사용하면 안됩니다.

```js
//script
const subscribeHTML = `<button onclick="document.querySelector('body').style.display='none'">구독</button>`;

//template
<div v-html='subscribeHTML'></div>;
```

---

## v-show

`v-show`는 화면에 태그를 생성해놓고 CSS display 속성을 전환합니다.
false가 되는 경우에는 `display: none;` 이 됩니다.

```js
//script
const display = true;

//template
<h2 v-show='display'>보입니다</h2>;
```

---

## v-bind

HTML 태그의 속성을 동적으로 변경하기 위해서 사용합니다.

```js
// script
const imageSource = 'https://placeimg.com/100/100/any';
const naverUrl = 'https://naver.com';

//template
<img v-bind:src="imageSource" alt="random" />
<a :href="naverUrl">naver로 바로가기</a> //v-bind 생략하고 :로 사용 가능
```

v-bind를 사용할 수 있는 대표적인 속성은 다음과 같습니다.

- 이미지 데이터 연결 v-bind:src
- 링크를 통한 연결 v-bind:href
- 키를 통한 연결 v-bind:key
- 스타일시트 연결 v-bind:class, v-bind:style

`class`나 `style` 속성을 바인딩하는 데 사용되는 경우 `배열`이나 `객체`로 값 유형을 추가할 수 있습니다.

```js
//example
//<h2 v-bind:class="{클래스명: 참/거짓}">{{ obj.subject }}를 좋아합니다.</h2>
<h2
  v-bind:class="{
    red: obj.subject === 'apple',
    'not-good': obj.subject === 'react',
  }"
>{{ obj.subject }}를 좋아합니다. </h2>

//style
.red {
	color: red;
}
.not-good {
	text-decoration: line-through;
}
```

---

## v-if, v-else-if, v-else

if / else if / else 문 구현하는 것입니다.
<template> 엘리먼트에 사용한 경우, 해당 컨텐츠가 조건부 블록으로 추출됩니다.
v-for 우선순위가 v-if 보다 높습니다.

```js
//script
const age = 20;

//template
<h2>당신의 나이는 {{ age }} 입니다.</h2>
<h3 v-if="age > 18">당신은 어른입니다.</h3>
<h3 v-else-if="age > 13 && age < 18">당신은 청소년입니다.</h3>
<h3 v-else>당신은 어린이입니다.</h3>
```

---

## v-for

원본 데이터 기준으로 엘리먼트를 여러번 렌더링 해주는 for문 입니다.
리스트 렌더링 되는 컴포넌트는 key라는 props가 필요합니다.
그 이유는 가상돔에서 리스트 컴포넌트에서 변경된 부분을 감지할 때 key라는 값을 이용하기 때문에 항상 key라는 값이 필요합니다.

key props를 사용하지 않는다면 아래와 같은 에러를 마주하게 됩니다.
`error Elements in iteration expect to have 'v-bind:key' directives`

### 반복과 조건

아래와 같은 예제에서는 배열의 모든 요소가 렌더링되지만 monkey는 화면에 보여지지 않습니다.

```js
//script
const animals = ['monkey', 'rat', 'dog', 'lion'];

//template
<h2 v-for="(el, idx) in animals" :key="idx">
  <span v-if="el !== 'monkey'"> {{ el }}. 인덱스는 {{ idx }} </span>
</h2>
```

불필요한 리스트를 제거하기 위해 <template> 태그를 사용했는데 <template> 태그는 key 처리가 될 수 없다는 에러가 발생했습니다.
`Errors <template> cannot be keyed. Place the key on real elements instead.`
해당 에러는 <h2> 태그에 idx값으로 key를 부여해서 해결할 수 있었습니다.

```js
<template v-for="(el, idx) in animals">
  <h2 v-if="el !== 'monkey'" :key="idx">{{ el }}. 인덱스는 {{ idx }}</h2>
</template>
```

### 중첩 반복

v-for와 v-if는 함께 사용할 수 없습니다.

```js
//script
const users = [
	{ name: 'chlo', job: 'dev', nationality: 'kr', skill: ['html', 'js', 'css'] },
	{
		name: 'david',
		job: 'designer',
		nationality: 'us',
		skill: ['html', 'js', 'css'],
	},
	{
		name: 'john',
		job: 'manager',
		nationality: 'ca',
		skill: ['html', 'js', 'css'],
	},
];

//template
<ul>
  <li v-for="(el, idx) in users" :key="idx">
    이름은 {{ el.name }}, 직업은 {{ el.job }}, 국적은 {{ el.nationality }}
    <p v-for="(skill, idx2) in el.skill" :key="idx2">{{ skill }}</p>
  </li>
</ul>
```

---

## v-pre

특정 엘리먼트를 무시하는데 사용됩니다. v-pre 디렉티브는 Vue 시스템ㅂ에서 해당 엘리먼트는 지시문이 없다는 것을 인식하여 그 엘리먼트 내부의 자식 엘리먼트들을 신경쓰지 않고 건너뛰게 됩니다. -> 컴파일 속도를 증가시킵니다.

## v-once

컴포넌트를 초기에 딱 한번만 렌더링해줍니다. 변동이 없고 정적인 부분을 보여줄 때 사용합니다.

## v-cloak

컴파일이 완료될 때까지 vue 인스턴스를 숨길 수 있습니다. 렌더링되지 않을 때 {{}}이 보였다가 로딩이 완료되면 내용이 출력될 때, 로딩이 완료되기 전까지 보이지 않게 할 때 사용 가능합니다.

> run을 계속 누르게 된다면 JS가 실행됩니다. JS 코드가 실행되기 이전이기 때문에 그 과정에서 숨겨놨던 엘리먼트들이 깜빡이는 현상이 생깁니다. Vue 인스턴스가 제대로 준비되기 전까지 템플렛을 위한 HTML 코드를 숨기고 싶을 때 사용하는 디렉티브입니다.

```css
<style>
  [v-cloak] { display: none; }
</style>
```

```js
<div id="app" v-cloak>
  <div>{{ name }}</div>
  <div>{{ age }}</div>
</div>

<script>
  var testApp = new Vue({
    el: "#app",
    data: {
      name: "vue",
      age: 28
    }
  });
</script>
```

---

# watch 속성

데이터 변화에 따라서 특정 로직을 실행할 수 있습니다.

```vue
<script>
new Vue({
	el: '#app',
	data: {
		num: 10,
	},
	watch: {
		//num이 바뀌면 logText함수를 실행해줌
		num: function () {
			this.logText();
		},
	},
	methods: {
		addNum: function () {
			this.num += 1;
		},
		logText: function () {
			console.log('changed');
		},
	},
});
</script>
```

## computed vs watch

computed : 단순한 값에 대한 계산할 때 사용됩니다. validation, 연산 등
watch : 매번 실행되는게 부담스러운 무거운 로직들에 사용됩니다. 데이터 요청 등

> 대부분의 케이스에 왠만하면 computed를 사용하는 것이 더 적합합니다. 불필요하게 watch를 남발하는 경우에 코드 가독성에 좋지 않습니다.
