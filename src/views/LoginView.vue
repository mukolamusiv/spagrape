<template>
  <div class="bg-page">
    <div class="form-wrap">
      <div class="form animate__animated animate__zoomIn">
        <div class="form-header">
          <img src="@/assets/img/logo.png" alt="">
        </div>
        <div v-if="data.signIn" class="form-signin">
          <div class="form-item">
            <label>
              <span class="material-icons">person</span>
              <input type="email" placeholder="email">
            </label>
          </div>
          <div class="form-item">
            <label>
              <span class="material-icons">lock</span>
              <input type="password" placeholder="password">
            </label>
          </div>
          <div class="login-error" v-if="data.error">
            Невірний логін, або пароль!
          </div>
          <div class="form-item login-btn c-pointer" @click="data.error = !data.error">
            Увійти
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { reactive } from 'vue'

const data = reactive({
  signIn: true,
  error: false
})

</script>

<style lang="scss" scoped>
.bg-page{
  display: flex;
   flex-wrap: nowrap;
   justify-content: center;
   height: 100vh;
   width: 100%;
  // background: linear-gradient(#ffdc76, #c58b67);
  background: linear-gradient(#7e78ff, #c17e55);
  background-image: url(@/assets/img/login-bg.jpg);
}
.form-wrap{
  width: 95%;
  max-width: 390px;
  display: flex;
  align-items: center;
  justify-content: center;
  .form{
    box-shadow: 0px 0px 50px 0px rgba(90,166,255,1);
    display: flex;
    align-items: center;
    justify-content: center;
    flex-wrap: wrap;
    width: 100%;
    padding: 32px;
    padding-top: 0;
    border-radius: 16px;
    background: #ffffff;
    .form-header{
      margin-top: -50px;
      margin-bottom: 31px;
      img{
        width: 100px;
      }
    }
    .form-signin{
      width: 100%;
    }
  }
}
.form-item{
  padding: 15px 0;
  width: 100%;
  display: flex;
  label{
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    border: 1px solid #92919c69;
    .material-icons{
      display: block;
      margin: -1px 0 -1px -1px;
      padding: 7px;
      color: #ffffff;
      font-size: 28px;
      background-color: #111111;
    }
    input{
      flex-grow: 1;
      padding: 8px;
      border: none;
      outline: none;
      display: block;
      line-height: 1.5rem;
      border-radius: 4px;
      font-size: 1rem;
      color: #111111;
      background-color: #ffffff;
    }
  }
}
.login-btn{
  margin-top: 32px;
  margin-bottom: 16px;
  display: block;
  text-align: center;
  padding: 8px 15px;
  border-radius: 16px;
  font-weight: bold;
  background-color: #111111;
  color: #acecd9;
}
.login-error{
  font-size: 0.8rem;
  font-style: italic;
  margin-top: -16px;
  position: absolute;
  color: red;
}
</style>
