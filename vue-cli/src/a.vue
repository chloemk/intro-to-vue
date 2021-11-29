<template>
	<div>
		<HelloWorld />
	</div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';

export default {
	//new Vue 인스턴스 만든 것과 같음. 인스턴스 옵션 속성 또는 컴포넌트 옵션 속성 넣어주면 됨.
	name: 'app',
	components: {
		HelloWorld,
		'hello-world': HelloWorld,
	},
};
</script>

<style></style>
