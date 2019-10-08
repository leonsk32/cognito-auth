<template>
  <div class="singin">
    <h1>Sign in</h1>
    <form @submit.stop.prevent="signIn" method="post">
      <p v-show="msg">{{ msg }}</p>
      <p v-show="errMsg">{{ errMsg }}</p>
      <input type="email" placeholder="Email" v-model="email" required>
      <input type="password" placeholder="Password" v-model="password" required>
      <input type="submit" value="Submit">
    </form>
    <p>Don't you have an account?
      <router-link :to="{ name: 'signup'}">Sign up now!!</router-link>
    </p>
  </div>
</template>

<script>
  import * as UserUtil from '@/utils/UserUtil';
  import * as AwsUtil from '@/utils/AwsUtil';

  export default {
    name: 'SignIn',
    props: ['flashMsg', 'flashErrMsg'],
    data() {
      return {
        email: '',
        password: '',
        errMsg: this.flashErrMsg,
        msg: this.flashMsg,
      };
    },
    methods: {
      async signIn() {
        try {
          await UserUtil.signIn(this.email, this.password);
        } catch(e) {
          this.errMsg = e.message;
        }
      },
    },
  };
</script>
