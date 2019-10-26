<template>
  <div id="login">
      <LoginForm @dataValidated="logIn" :matched="matched"/>
  </div>
</template>

<script>
import LoginForm from '../components/LoginForm.vue';

const loginData = [
  { role: 'Student', login: 'student', pass: 'sdemo' },
  { role: 'Teacher', login: 'teacher', pass: 'tdemo' }
];

export default {
    data() {
      return {
        loginData,
        matched: true
      }
    },

    methods: {
      logIn(login, pass){
        for(let i = 0; i < this.loginData.length; i++){
          if(this.loginData[i].login !== login) continue;
          if(this.loginData[i].pass !== pass) continue;
          this.matched = true;

          switch(this.loginData[i].role){
            case "Student":
              this.$router.push("student");
              break;
            case "Teacher":
              this.$router.push("teacher");
              break;
          }

          return;
        }
        this.matched = false;
      }
    },

    components: { LoginForm }
}
</script>

<style>

</style>