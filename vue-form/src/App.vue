<template>
	<form v-on:click.prevent="submitForm">
		<div>
			<label for="username">아이디: </label>
			<input id="username" type="text" v-model="username" />
		</div>
		<div>
			<label for="password">패스워드: </label>
			<input id="password" type="password" v-model="password" />
		</div>
		<button type="submit">로그인</button>
	</form>
</template>

<script>
import axios from 'axios';

export default {
	data: function () {
		return {
			username: '',
			password: '',
		};
	},
	methods: {
		submitForm: function () {
			console.log(this.username, this.password);
			//폼의 기본동작(폼을 제출하고 어떤 페이지로 넘어가서 새로고침되는 속성) 새로고침을 막음
			const url = 'https://jsonplaceholder.typicode.com/users';
			const data = {
				username: this.username,
				passowrd: this.password,
			};
			axios
				.post(url, data)
				.then((res) => console.log(res))
				.catch((err) => console.log(err));
		},
	},
};
</script>

<style>
* {
	margin: 0;
	box-sizing: border-box;
	font-size: 20px;
}

form {
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
	width: 60%;
	height: 100vh;
	margin: 0 auto;
	border: 1px solid #000;
}
</style>
