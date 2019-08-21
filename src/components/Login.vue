<template lang="pug">
  div
    h2 Login
    form(@submit.prevent)
      .form-group
        label(for='username') Username
        input.form-control(type='text'  v-model='username' autocomplete="off" name='username')
      .form-group
        label(htmlfor='password') Password
        input.form-control(type='password' autocomplete="off" v-model='password' name='password') 
      .form-group
        button.btn.btn-primary( @click="login") Login
</template>

<script>
export default {
   data () {
      return {
          username: '',
          password: '',
      }
    },
    methods: {
      login() {
        let vm = this
        let name = "aris"
        let pass = "password"
        if(this.username != "" && this.password != "") {
            if(this.username === "aris" && this.password === "password") {
                this.$router.replace({ name: "winebeer" });
            } else {
                alert("Username and Password is incorrect!")
            }
        } else {
            alert("Username and Password should have values!")
        }
      },
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import "@/assets/scss/mixins.scss";
.form-group {
  width:300px;
  display: flex;
  flex-direction: row;
  flex-basis: 100%;
  justify-content: flex-end;
  margin:10px auto;
  label {
    flex: 1;
  }
  input {
    flex:2;
    height:30px;
    padding:0 10px;
    margin-left:10px;
    border:2px solid #ef506e;
    @include border-radius(5px);
  }
  button {
    width:100%;
    height:50px;
    color:#fff;
    margin:20px auto;
    font-size:16px;
    text-align:center;
    background: #ef506e;
    @include border-radius(5px);
  }
  .error {
    font-size:12px;
    color:red;
    margin:10px auto;
    text-align:center;
  }
}
</style>
