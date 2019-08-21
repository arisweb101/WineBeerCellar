<template>
  <div class="wine-beers container">
     <a href="/"><img alt="Vue logo" class="logo" src="../assets/images/logo.png"></a>
    <AddBeerModal />
    <WineBeer />
  </div>
</template>
<script>
// @ is an alias to /src
import WineBeer from '@/components/WineBeerList'
import AddBeerModal from '@/components/AddBeerModal'
export default {
  components: {
    WineBeer,
    AddBeerModal
  },
}
</script>

<style scoped lang="scss">
.logo {
  width:250px;
  margin:50px 0 0;
}
</style>
