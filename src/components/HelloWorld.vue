<template>
  <div class="hello">
    <form @submit.prevent="createUser" method="post">
      <div>
        <label for="userName">userName</label>
        <input type="text" v-model="formData.UserName">
      </div>
      <div>
        <label for="email">Email</label>
        <input type="text" v-model="formData.Email">
      </div>
      <div>
        <label for="password">Password</label>
        <input type="password" v-model="formData.Password">
      </div>
      <div>
        <label for="confirmedPassword">Confirm Password</label>
        <input type="password" v-model="formData.ConfirmPassword">
      </div>
      <button>Submit</button>
      {{users}}
    </form>
  </div>
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
        .then((response)=> console.log(response))
        .catch((error)=> console.log(error))
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
