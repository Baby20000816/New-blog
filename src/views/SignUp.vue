<template>
	<div id="bg">
		<router-link to="/index"><h2>首页</h2></router-link>
		<div class="login-box">
			
			<form class="login-form">
				手机号:<input type="text" v-model="userDto.mobile" id="mobile" />
				密码:<input type="password" v-model="userDto.password" />
				称呼:<input type="nickname" v-model="userDto.nickname" />
				性别:<input type="gender" v-model="userDto.gender" />
				生日(例2019-12-2):<input type="datetime-local" v-model="userDto.birthday" placeholder="YYYY-MM-DD"/>
				<!-- <input type="datetime-local" class="" placeholder="YYYY-MM-DD" v-model="userDto.birthday" > -->
				<input type="button" class="btn btn-lg dark-fill" value="注册" @click="signUp(userDto)" />
				<router-link to="/sign-in">已有账号？去登录</router-link>
			</form>
		</div>
	</div>
</template>
<script>
export default {
	data() {
		return {
			userDto: {
				mobile: '',
				password: '',
				nickname:'',
				gender:'',
				
				
			}
		};
	},
	created() {
		var number = Math.ceil(Math.random() * 10);
		this.codeUrl = this.GLOBAL.baseUrl + '/code?num = ' + number;
	},
	methods: {
		signUp(userDto) {
			this.axios({
				method: 'post',
				url: this.GLOBAL.baseUrl + '/user/sign-up',
				data: JSON.stringify(this.userDto)
			}).then(res => {
				if (res.data.msg === '成功') {
					alert('注册成功');
					this.$router.push('/sign-in');
				} else {
					alert(res.data.msg);
				}
			});
		}
	}
};
</script>
<style scoped>
	
#bg {
	position: absolute;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
	background-image: url(../assets/img/bg.jpg);
}
.login-box {
	width: 450px;
	height: 500px;
	border: 2px solid rgb(73, 137, 244);
	border-radius: 10px;
	background-color: rgb(73, 137, 244, 0.6);
	position: absolute;
	top: 80px;
	left: 30%;
}
.login-form {
	padding-top: 20px;
	width: 70%;
	margin: 0 auto;
	text-align: left;
}
.login-form input {
	width: 100%;
	height: 35px;
	outline: none;
	border: none;
	margin-bottom: 20px;
	border-radius: 5px;
}
</style>
