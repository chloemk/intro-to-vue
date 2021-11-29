# [5] Vue Router

SPA를 구현할 때 페이지간의 이동을 위해 사용하는 라이브러리 입니다.

---

## CDN으로 설치

```html
<script src="https://unpkg.com/vue/dist/vue.js"></script>
<script src="https://unpkg.com/vue-router/dist/vue-router.js"></script>
```

## NPM으로 설치

```
npm install vue-router
```

---

# Vue 라우터 등록 및 라우터 옵션

옵션

- mode : URL의 해쉬 값(#) 제거 속성입니다. #이 없어지면서 조금 더 깔끔한 url을 구현할 수 있습니다.
  `mode: 'history'`
- routes : 라우팅 할 URL과 컴포넌트 값을 지정합니다.

```js
//컴포넌트
var LoginComponent = {
	template: '<div>여긴 로그인 컴포넌트</div>',
};

// 라우터 인스턴스 생성
var Router = new VueRouter({
	//라우터 옵션
	//페이지의 라우팅 정보가 배열로 담기고, 페이지 갯수만큼 객체로 담긴다.
	routes: [
		//로그인 페이지 정보
		{
			//페이지의 url 이름
			path: '/login',
			//해당 url에서 표시될 컴포넌트
			component: LoginComponent,
		},
	],
	mode: 'history',
});

new Vue({
	//new Vue라고 하는 인스턴스에 #app이라는 id에 인스턴스를 정의함
	el: '#app',
	//인스턴스에 라우터 인스턴스 등록
	router: Router,
});
```

---

# router-view

페이지 url이 변경됬을 때 url에 따라 해당 컴포넌트를 뿌려주는 영역입니다.
router 인스턴스에서 정의한 path에 따라서 router-view가 변경됩니다.
Vue 인스턴스에 router 인스턴스를 연결해야지만 사용할 수 있는 태그입니다.

```html
<div id="app">
	<router-view></router-view>
</div>
```

# router-link

페이지 이동을 위한 링크 태그입니다.
router-link는 화면에 `<a>` 태그로 변환되서 나타납니다.

```html
<div id="app">
	<div>
		<router-link to="/이동할 url"></router-link>
		<router-link to="/login">Login</router-link>
	</div>
</div>
```
