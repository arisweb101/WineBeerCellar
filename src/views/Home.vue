<template>
  <div class="home">
    <a href="/"><img alt="Vue logo" src="../assets/images/logo.png"></a>
    <Login/>
  </div>
</template>
<script>
// @ is an alias to /src
import Login from '@/components/Login'

export default {
  name: 'home',
  components: {
    Login
  },
}
</script>

<style scoped lang="scss">
.home {
  width:100%;
}
</style>
