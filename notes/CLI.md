# [7] Vue CLI

## 글로벌에 설치

`npm install -g @vue/cli`

Webpack은 서로 연관 관계가 있는 웹 자원들을 static한 자원으로 변환해주는 모듈 번들러입니다.

## 프로젝트 시작하기

`vue create '폴더 위치'`

## 로컬 서버 실행하기

`npm run serve `

template 속성을 정의했을 때 render 함수가 실행된다.

## 자동완성

` vue`

---

CLI를 통해서 .vue 파일을 만들면 컴포넌트들을 재사용할 확률이 높습니다. 여러개의 컴포넌트에서 동일한 값을 공유/참조하면 안되기 때문에 data: {} 객체 리터럴이 아닌, 함수를 연결해준 후, 새 객체를 반환해줘야합니다.

```js
export default {
	// data: {

	// }
	data: function () {
		return {};
	},
};
```
