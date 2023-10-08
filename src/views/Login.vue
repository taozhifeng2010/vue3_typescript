<!-- src/view/Login.vue 登录页面 -->
<template>
  <div class="login">
    <div class="loginTitle">
      <div>
        <span class="iconfont icon-taozi"></span>
        <span>tao</span>
      </div>
      <div>
        <span @click="localeFn" >{{ state.locale === "en" ? "中文" : "English" }}</span> <!-- 中英文切换-->
      </div>
    </div>
    <div class="loginFrom">
      <div class="from">
        <div class="title">登录页面</div>
        <a-form
          :model="formState"
          name="basic"
          :label-col="{ span: 8 }"
          :wrapper-col="{ span: 16 }"
          autocomplete="off"
          @finish="onFinish"
        >
          <a-form-item
            label="用户名"
            name="username"
            :rules="[{ required: true, message: '请输入用户名!' }]"
          >
            <a-input v-model:value="formState.username" />
          </a-form-item>

          <a-form-item
            label="密码"
            name="password"
            :rules="[{ required: true, message: '请输入密码!' }]"
          >
            <a-input-password v-model:value="formState.password" />
          </a-form-item>

          <a-form-item name="remember" style="display: flex;justify-content: center;text-align: center">
            <a-checkbox v-model:checked="formState.remember">记住登录</a-checkbox>
          </a-form-item>

          <a-form-item style="display: flex;justify-content: center;text-align: center">
            <a-button type="primary" html-type="submit">登录</a-button>
          </a-form-item>
          <a-form-item style="display: flex;justify-content: center;text-align: center">
            <span>没有账户？请注册</span> <!-- 用来跳转到注册页面 -->
          </a-form-item>
        </a-form>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>

import { reactive } from 'vue';

interface FormState {
  username: string;
  password: string;
  remember: boolean;
}

let state=reactive({locale:'zh'}) // 必须这样写，不然页面刷新

const formState = reactive<FormState>({
  username: '',
  password: '',
  remember: true,
});

const localeFn=()=>{   // 显示中英文切换
  if(state.locale==='zh'){
    state.locale='en'
  }else{
    state.locale='zh'
  }
}

const onFinish = (values: FormState) => {  // 表单提交
  console.log('Success:', values);
  if(values.username==='tao'){
    if(values.password==='admin123'){
      alert('登录成功')
      window.location.href='/home'
    }else{
      alert('密码错误')
    }
  }else{
    alert('用户名错误')
  }
};

</script>

<style lang="less">
.login {
  width: 100%;
  height: 100%;
  padding: 10px;
  display: flex;
  flex-direction: column;
  .loginTitle {
    height: 40px;
    display: flex;
    padding: 0 40px;
    justify-content: space-between;
    .icon-taozi {
      color: pink;
    }
  }
  .loginFrom {
    flex: 1;
    padding: 0 5px;
    display: flex;
    align-items: center;
    justify-content: center;
    .from {
      border-radius: 10px;
      padding: 20px;
      box-shadow: 5px 5px 15px pink;
      display: flex;
      align-items: center;
      flex-direction: column;
      .title {
        margin-bottom: 20px;
        font-size: 18px;
        line-height: 20px;
      };
    }
  }
}
</style>

