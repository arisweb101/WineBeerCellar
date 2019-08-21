<template lang="pug">
  div
    b-modal#modal-add-beer.form-group(ref="add-beer" title="Add Beer" v-bind:hide-footer="true")
      div.form-group
        label Name
        input.name(v-model="beer.name" required)
      div.form-group
        label Brewery Type
        input.brewery_type(v-model="beer.brewery_type" required)
      div.form-group
        label State
        input.state(v-model="beer.state" required)
      div.form-group
        label Country
        input.country(v-model="beer.country" required)
      div.form-group
        label Website Url
        input.website_url(v-model="beer.website_url" required)
      b-button.btn-danger(block @click="addBeer()") Add
      b-button.mt-3(block @click="hideModal()") Cancel
</template>

<script>
import axios from 'axios'
import eventBus from "../eventbus";
export default {
   data () {
      return {
        add: false,
        beerList: '',
        beer: {
          name: '',
          brewery_type: '',
          state: '',
          country: '',
          website_url: ''
        },
      }
    },
    mounted() {
      eventBus.$on("openModal", add => {
        this.$refs['add-beer'].show()
      });
    },
    methods: {
      hideModal() {
        this.$refs['add-beer'].hide()
        this.beer = {}
      },
      addBeer() {
        eventBus.$emit("createdBeer", this.beer);
        this.hideModal()
      }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import "@/assets/scss/mixins.scss";

.form-group {
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
}
</style>
