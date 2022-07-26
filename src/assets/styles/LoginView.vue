<template>
  <div class="bg-login">
    <div class="form-signin-wrap">
      <div class="form-signin">
        <div class="form-item">
        <label>ваш логін</label>
        <input type="text" v-model="login" v-bind:class="{ loginError: loginError }" @keyup.enter="authorization">
        </div>
        <div class="form-item">
        <label>ваш пароль</label>
        <input type="password" v-model="password" v-bind:class="{ loginError: loginError }" @keyup.enter="authorization">
        </div>
        <button type="button" name="button" @click="authorization">Вхід</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import axios from 'axios'
import { useStore } from '@/store'

const router = useRouter()
const { store } = useStore()
const login = ref()
const password = ref()
const loginError = ref()
const authorization = function () {
  // const formData = new FormData()
  // formData.append('name', 'bjbjbj')
  axios({
    method: 'POST',
    url: '/login',
    data: {
      action: 'login',
      login: login.value,
      password: password.value
    }
  }).then(function (response) {
    console.log(response.data)
    if (response.data.access === true) {
      store.access = response.data.access
      store.user.id = response.data.id
      store.user.name = response.data.name
      store.user.type = response.data.type
      const payload = `{
      "user_type": "${response.data.type}",
      "user_session": "${response.data.session}",
      "user_id": "${response.data.id}"
      }`
      store.token = btoa(payload)
      localStorage.token = store.token
      localStorage.name = response.data.name
      localStorage.type = response.data.type
      axios.defaults.headers.common['Authorization'] = store.token
      router.push('/')
    }
    if (response.data.loginError === true) {
      loginError.value = true
    }
  })
}
</script>

<style lang="scss" scoped>
input:focus{
  border-bottom: 2px solid #2099DD;
}
input{
  width: 100%;
  font-size: 0.9rem;
  border-bottom: 2px solid #19DDDC;
}
label{
  color: #1f9adc;
  margin-left: 10px;
  font-style: italic;
  font-size: 0.7rem;
}
button{
  margin-left: auto!important;
}
.form-item{
  margin-bottom: 15px;
  width: 100%;
}
.form-signin-wrap {
  display: flex;
  max-width: 320px;
  width: 100%;
  align-items: center;
  justify-content: center;
  height: calc(100% - 75px);
  .form-signin{
    width: 100%;
    padding: 16px;
    border-radius: 16px;
    background: #ffffff;
  }
}
.bg-login{
  display: flex;
   flex-wrap: nowrap;
   justify-content: center;
   height: 100vh;
   width: 100%;
  background: linear-gradient(#2099DD, #19DDDC);
}
button{
  display: block;
  padding: 8px 16px;
  font-size: 1rem;
  font-weight: 600;
  outline:none!important;
  -webkit-appearance: none;
  border-radius: 12px;
  border: 0;
  background: #1f99dc;
  color: #ffffff;
}
button:hover{
  background: #1a7cb1;
}
</style>
