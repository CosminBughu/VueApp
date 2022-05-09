<template>
<form @submit.prevent="createUser" method="post">
  <div id="login-box">
    <div class="left">
      <h1>Sign up</h1>
      <input type="text" name="username" placeholder="Username" v-model="formData.UserName"/>
      <input type="text" name="email" placeholder="E-mail" v-model="formData.Email"/>
      <input type="password" name="password" placeholder="Password" v-model="formData.Password"/>
      <input type="password" name="password2" placeholder="Retype password" v-model="formData.ConfirmPassword"/>
      <input type="submit" name="signup_submit" value="Sign me up" />
    </div>
    <div class="or">OR</div>
    <div class="right">
      <span class="loginwith">Sign in with<br />social network</span>
      <button class="social-signin facebook">Log in with facebook</button>
      <button class="social-signin google">Log in with Google+</button>
    </div>
  </div>
</form>
</template>

<script>
import axios from 'axios'
export default {
  name: 'HelloWorld',
  data() {
    return {
      formData:{
        UserName: '',
        Email: '',
        Password: '',
        ConfirmPassword: '',
      },
      users: null
    }
  },
  mounted() {
     axios.get('https://localhost:7006/api/account/users')
       .then((users)=> console.log(users))
        .catch((error)=> console.log(error))
  },
  methods: {
    createUser(){
      const data = JSON.stringify(this.formData);
      const options = {headers: {"content-type": "application/json"}}
      axios.post('https://localhost:7006/api/account/signup', data,options)
        .then((response)=> console.log(response),
          this.formData.UserName = "",
          this.formData.Email = "",
          this.formData.Password = "",
          this.formData.ConfirmPassword = "",
        )
        .catch((error)=> console.log(error))
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
*:focus {
  outline: none;
  background-color: #E0FFFF;
}
#login-box {
  position: relative;
  margin: 5% auto;
  width: 50%;
  height: 400px;
  background: #FFF;
  border-radius: 2px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.4);
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

.left {
  position: absolute;
  top: 0;
  left: 0;
  box-sizing: border-box;
  padding: 40px;
  width: 300px;
  height: 400px;
}

h1 {
  margin: 0 0 20px 0;
  font-weight: 300;
  font-size: 28px;
}

input[type="text"],
input[type="password"] {
  display: block;
  box-sizing: border-box;
  margin-bottom: 20px;
  padding: 4px;
  width: 220px;
  height: 32px;
  border: none;
  border-bottom: 1px solid #AAA;
  font-family: 'Roboto', sans-serif;
  font-weight: 400;
  font-size: 15px;
  transition: 0.2s ease;
}

input[type="text"]:focus,
input[type="password"]:focus {
  border-bottom: 2px solid #16a085;
  color: #16a085;
  transition: 0.2s ease;
}

input[type="submit"] {
  margin-top: 28px;
  width: 120px;
  height: 32px;
  background: #16a085;
  border: none;
  border-radius: 2px;
  color: #FFF;
  font-family: 'Roboto', sans-serif;
  font-weight: 500;
  text-transform: uppercase;
  transition: 0.1s ease;
  cursor: pointer;
}

input[type="submit"]:hover,
input[type="submit"]:focus {
  opacity: 0.8;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.4);
  transition: 0.1s ease;
}

input[type="submit"]:active {
  opacity: 1;
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.4);
  transition: 0.1s ease;
}

.or {
  position: absolute;
  top: 180px;
  left: 340px;
  width: 40px;
  height: 40px;
  background: #DDD;
  border-radius: 50%;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.4);
  line-height: 40px;
  text-align: center;
}

.right {
  position: absolute;
  top: 0;
  right: 0;
  box-sizing: border-box;
  padding: 40px;
  width: 300px;
  height: 400px;
  background: url('../../public/image.jpg');
  background-size: cover;
  background-position: center;
  border-radius: 0 2px 2px 0;
}

.right .loginwith {
  display: block;
  margin-bottom: 40px;
  font-size: 28px;
  color: #FFF;
  text-align: center;
}

button.social-signin {
  margin-bottom: 20px;
  width: 220px;
  height: 36px;
  border: none;
  border-radius: 2px;
  color: #FFF;
  font-family: 'Roboto', sans-serif;
  font-weight: 500;
  transition: 0.2s ease;
  cursor: pointer;
}

button.social-signin:hover,
button.social-signin:focus {
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.4);
  transition: 0.2s ease;
}

button.social-signin:active {
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.4);
  transition: 0.2s ease;
}

button.social-signin.facebook {
  background: #32508E;
}

button.social-signin.google {
  background: #DD4B39;
}
</style>