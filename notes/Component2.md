# [4] Vue 컴포넌트 통신 규칙

모든 컴포넌트 인스턴스에는 각자 고유한 유효범위(scope)를 가지고 있습니다. 때문에 다른 컴포넌트의 데이터를 직접적으로 참조할 수 없습니다.
각각의 컴포넌트는 데이터를 관리하고 공유하기 위해서는 props 속성 전달과 이벤트 전달방식을 이용 해야합니다.

인스턴스에서 정의한 (루트에 있는) 데이터 내용을 props로 하위 컴포넌트에게 전달할 수 있다. 상위 컴포넌트 데이터 내용을 바꾸면 하위 컴포넌트도 반영되고, 그리고 전달된 값이 화면에 바로 반영됩니다. 이것이 reactivity 입니다.

## 양방향 통신의 문제점

특정 데이터가 바뀌었을 때 그로 인한 버그를 추척하기가 어렵습니다.

## 컴포넌트의 통신방식이라는 규칙이 생겼을 때의 이점

데이터의 흐름을 추적할 수 있습니다. 항상 데이터는 내려오고, 아래에서 위로는 이벤트가 올라가게됩니다.

---

# 상위 -> 하위 컴포넌트 데이터 내려줌 (props 속성)

하위 컴포넌트에 속성을 정의하게 됩니다.
아래의 예제에서는 상위 컴포넌트(root)에서 하위 컴포넌트(app header)로 props를 넘겨줍니다.
`v-bind`를 이용하면 동적으로 prop 전달이 가능합니다.
` <app-header v-bind:프롭스속성이름='상위 컴포넌트의 데이터 이름'></app-header>`

```js
//script
var appHeader = {
  //props: ['프롭스 속성이름']
  props: ['propsdata'],
  template: '<h1>{{ propsdata }}</h1>',
};
new Vue({
  el: '#app',
  components: {
    'app-header': appHeader,
  }
  data: {
    message: 'hi',
  },
})

//template
<div id='app'>
  <app-header v-bind:propsdata="message"></app-header>
</div>
```

상위 데이터 속성 값이 변경되면, 변경된 데이터가 그대로 하위 컴포넌트에도 반영이 됩니다. 이것을 통해 Reactivity가 props에도 그대로 반영이 된다는 사실을 알 수 있습니다.

---

# 하위 -> 상위 이벤트 올려줌 (이벤트 발생)

하위 컴포넌트에서 특정 이벤트가 발생하면 상위 컴포넌트로 신호를 보냅니다. `(event emit)`
상위 컴포넌트에서는 하위 컴포넌트의 특정 이벤트가 발생되기를 기다리다가 해당 이벤트를 수신하여 데이터를 처리합니다.

```
발생 (하위 컴포넌트): $emit()
this.$emit('이벤트 명');

수신 (상위 컴포넌트): v-on
<app-header v-on:하위 컴포넌트에서 발생한 이벤트 이름='상위 컴포넌트의 메서드 이름'></app-header>
```

```js
//하위 컴포넌트. vue.js에서 제공되는 API인 $emit을 이용하여 update라는 이벤트를 발생시킨다.
var = childComponent {
  methods: {
    sendEvent: function() {  //1.자식 컴포넌트에서 sendEvent() 메서드가 실행되면
      this.$emit('update') //2.update라는 이벤트가 발생되고
    }
  }
}

//예제의 경우 상위 컴포넌트(root)가 된다.
//자식으로부터 올라온 이벤트를 상위 컴포넌트에서 받을 수 있게 해야한다.
new Vue({
  el: '#app',
  components: {
    'child-comp': childComponent
  },
  methods: {
    showAlert: function () {
      alert('이벤트 수신이 완료되었습니다!')
    }
  }
})

//template
//
<div id="app">
  <child-component v-on:update="showAlert"></child-component>
</div>

```

---

# 같은 컴포넌트 레발 간의 통신 방법 (이벤트 버스)

상위 -> 하위는 props로, 하위 -> 상위로는 이벤트 발생을 통해 통신했습니다.
같은 레벨의 컴포넌트끼리는 컴포넌트 고유의 유효범위 때문에 통신이 되지 않습니다. 따라서 공통 상위 컴포넌트로 이벤트를 올려준 후, 하위 컴포넌트에게 props로 데이터를 내려주는 방식으로 통신해야합니다. 그리고 이러한 통신 방식을 `이벤트 버스`라고 합니다.

> 이벤트 버스의 장/단점
> 장점 : 컴포넌트간 데이터 전달이 가능해집니다.
> 단점 : 컴포넌트가 많아지면 어디로 보냈는지 관리가 되지 않습니다.

---

# this

객체안의 속성에서 다른 속성을 this로 가르키면, 그 this는 변수 선언된 obj를 바라보게 됩니다.

```js
var obj = {
	num: 10,
	getNumber: function () {
		console.log(this.num);
	},
};

obj.getNumber(); // 10
```

```js
var Vue = {
	el: '',
	data: {
		num: 10,
	},
	methods: {
		getNumber: function () {
			this.num; //this는 Vue 객체 data의 num 속성을 바라보게 된다.
		},
	},
};
```
