<template>
  <div class="container1">
        <div class="top"></div>
        <div class="bottom"></div>
        <div class="center">
          <h2>Please Sign In</h2>
          <input type="email" placeholder="email" v-model="email"/>
          <input type="password" placeholder="password" v-model="password"/>
          <button @click.prevent="login">login</button>
        </div>
      </div>
</template>

<script>
import axios from '../axios'
export default {
  name: 'login',
  data () {
    return {
      email: '',
      password: ''
    }
  },
  methods: {
    login () {
      axios({
        method: 'POST',
        url: '/user/login',
        data: {
          email: this.email,
          password: this.password
        }
      })
        .then(result => {
          localStorage.setItem('token', result.data.token)
          localStorage.setItem('email', this.email)
          this.$router.push('home/category/tablecategory')
        })
        .catch(err => {
          if (err) {
            this.$toasted.global.my_app_error({
              message: 'Username/Password not Found'
            })
          }
        })
    }
  },
  created () {
    if (localStorage.token) {
      this.$router.push('home/category/tablecategory')
    }
  }
}
</script>
<style>
@import url("https://fonts.googleapis.com/css?family=Raleway:400,700");
*, *:before, *:after {
  box-sizing: border-box;
}

body {
  min-height: 100vh;
  font-family: 'Raleway', sans-serif;
}

.container1 {
  position: absolute;
  width: 100%;
  height: 100%;
  overflow: hidden;
}
.container1:hover .top:before, .container1:hover .top:after, .container1:hover .bottom:before, .container1:hover .bottom:after, .container1:active .top:before, .container1:active .top:after, .container1:active .bottom:before, .container1:active .bottom:after {
  margin-left: 200px;
  transform-origin: -200px 50%;
  transition-delay: 0s;
}
.container1:hover .center, .container1:active .center {
  opacity: 1;
  transition-delay: 0.2s;
}

.top:before, .top:after, .bottom:before, .bottom:after {
  content: '';
  display: block;
  position: absolute;
  width: 200vmax;
  height: 200vmax;
  top: 50%;
  left: 50%;
  margin-top: -100vmax;
  transform-origin: 0 50%;
  transition: all 0.5s cubic-bezier(0.445, 0.05, 0, 1);
  z-index: 10;
  opacity: 0.65;
  transition-delay: 0.2s;
}

.top:before {
  transform: rotate(45deg);
  background: #e46569;
}
.top:after {
  transform: rotate(135deg);
  background: #ecaf81;
}

.bottom:before {
  transform: rotate(-45deg);
  background: #60b8d4;
}
.bottom:after {
  transform: rotate(-135deg);
  background: #3745b5;
}

.center {
  position: absolute;
  width: 400px;
  height: 400px;
  top: 50%;
  left: 50%;
  margin-left: -200px;
  margin-top: -200px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 30px;
  opacity: 0;
  transition: all 0.5s cubic-bezier(0.445, 0.05, 0, 1);
  transition-delay: 0s;
  color: #333;
}
.center input {
  width: 100%;
  padding: 15px;
  margin: 5px;
  border-radius: 1px;
  border: 1px solid #ccc;
  font-family: inherit;
}
</style>
