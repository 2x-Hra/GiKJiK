<template>
	<v-app>
		<v-container class="fill-height grey lighten-4" fluid>
			<v-row align="center" justify="center">
				<v-col cols="12" sm="8">
					<v-card class="elevation-12">
						<v-window v-model="step">
							<v-window-item :value="1">
							<v-row>
								<v-col cols="12" md="8">
								<v-card-text class="mt-12">
									<h1 class="text-center display-2 teal--text text--accent-4"> <span class="font-weight-light ">GIK</span><span>JIK</span></h1>
									<div class="text-center" mt-4>
										
									
									</div>
									<!-- <h4 class="text-center mlt-4">Ensure your Username for resitration</h4> -->
									<v-form>
									<v-text-field 
									label="Username"
									name="username"
									prepend-icon="person"
												v-model="username"
									type="text"
									color="teal accent-4">
									</v-text-field>
									<v-text-field
									id="password"
												v-model="password"
									label="Password"
									name="Password"
									prepend-icon="lock"
									type="password"
									color="teal accent-4" />

									</v-form>
									<!-- <h3 class="text-center mt-3">Forget your password?</h3> -->

								</v-card-text>
								<div class="text-center mt-3">
									<v-btn rounded color="teal accent-4" dark @click="signin">SIGN IN</v-btn>
								</div> 
								</v-col>
								<v-col cols="12" md="4" class="teal accent-4">
								<v-card-text class="white--text mt-12">
									<h1 class="text-center display-3">
									Hello, friends !

									</h1>

									<h5 class="text-center">Enter your personal details and start journay</h5>

								</v-card-text>
								<div class="text-center">
									<v-btn rounded outlined="" dark @click="step++"> 
									SIGN UP
									</v-btn>

								</div>

								</v-col>
							</v-row>
							</v-window-item>
							<v-window-item :value="2">
							<v-row class="fill-height">
								<v-col cols="12" md="4" class="teal accent-4">
								<v-card-text class="white--text mt12">
									<h1 class="text-center display-1">Welcome Back !</h1>
									<h5 class="text-center">To Keep connected with us please login with your personal information</h5>
								
								</v-card-text>
									<div class="text-center">
									<v-btn rounded outlined dark @click="step--">SIGN IN</v-btn>
									</div>
								</v-col>
								<v-col cols="12" md="8">
								<v-card-text class="mt-12">
									<h1 class="text-center display-2 teal--text text--accent-4">Create Account</h1>
									<div class="text-center mt-4">
									
									</div>
									<!-- <h4 class="text-center mt-4">Ensure your Email for registration</h4> -->
									<v-form>
									<v-text-field
									label="Username"
									name="Name"
												v-model="username"
									prepend-icon="person"
									type="text"
									color="teal accent-4">
									</v-text-field>

									<v-text-field
									label="Email"
									name="Email"
												v-model="email"
									prepend-icon="email"
									type="text"
									color="teal accent-4" />
									<v-text-field
									label="Password"
									name="Password"
									v-model="password"
									prepend-icon="lock"
									type="password"
									color="teal accent-4" />
									</v-form>
								</v-card-text>
								<div class="text-center mt-5">
									<v-btn rounded color="teal accent-4" dark @click="signup">SIGN UP</v-btn>

								</div>

								</v-col>
							</v-row>
							</v-window-item>
						</v-window>
					</v-card>
				</v-col>
			</v-row>
		</v-container>
	</v-app>
</template>

<script>
import axios from 'axios'
  export default {
    data: () =>({
		username:'',
		email:'',
		password:'',
		token:'',
      step: 1
    }),
    props:{
      source: String
	},
	
	
    methods:{
		signup:function(){
			axios.post('http://127.0.0.1:8000/sign-up/', {
				username: this.username,
				email: this.email,
				password: this.password
			}).then((response) =>{
				let token = response.data.access;
				localStorage.setItem("LearnOnlineToken", 'Bearer ' + token);
				axios.defaults.headers.common['Authorization'] = 'Bearer ' + token;
				window.location.reload()
			
				})
			
		},
		signin:function() {
			axios.post('http://127.0.0.1:8000/log-in/',{
				username: this.username,
				password: this.password,
			})
			.then( (response) => {
				
				let token = response.data.access;
				localStorage.setItem("LearnOnlineToken", 'Bearer ' + token);
				axios.defaults.headers.common['Authorization'] = 'Bearer ' + token;
				(this.$router.push({name:'User'}));
				
				})
		},
		move:function(){
			
			this.$router.push({name:'User'});
			
		}
    }
  };
</script>