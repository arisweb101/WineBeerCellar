<template lang="pug">
  div 
    h1 Wine and Beer Brewery
    .searchForm Search
       input.search(type='text' v-model='searchBeer' placeholder='Search Beer Name')
    b-button.add-beer(v-b-modal.modal-1 @click="openAddBeerModal") Add Beer
    table
      thead
        tr
          th( @click="sortBy('name')") Name
          th( @click="sortBy('brewery_type')") Brewery Type
          th( @click="sortBy('state')") State
          th( @click="sortBy('country')") Country
          th( @click="sortBy('website_url')") Website_url
        tr(v-for="beer in filteredBeers") 
          td {{ beer.name }}
          td {{ beer.brewery_type }}
          td {{ beer.state }}
          td {{ beer.country }}
          td {{ beer.website_url }}
</template>
<script>
import axios from 'axios'
import eventBus from "../eventbus";
export default {
  data () {
    return {
      beers: [],
      sortCat: 'name',
      sortDirection: 'asc',
      searchBeer: '',
      openModal: false,
      createdBeer: false
      }
  },
  mounted() {
    let vm = this
    eventBus.$on("createdBeer", created => {
        vm.beers.push(created)
        setTimeout(() => {
           alert("Added Beer! But the data wound not be store on the API")
        }, 500);
      });
  },
  created () {  
    this.showBeers()
  },
  methods: {
    showBeers() {
      let vm = this;
      let baseURL = 'https://api.openbrewerydb.org/breweries';
        // Set base url for api calls
      axios.get(baseURL)
           .then(response => {
            vm.beers = response.data
         }).catch(error => {
            alert(error)
      })
    },
    sortBy(cat) {
      if(cat === this.sortCat) {
        this.sortDirection = this.sortDirection === 'asc' ? 'desc':'asc';
      }
      this.sortCat = cat;
    },
    openAddBeerModal() {
      this.openModal = true
      eventBus.$emit("openModal", this.openModal)
      this.searchBeer = ''
    }
  },
  computed: {
    filteredBeers() {
      let vm = this
      return this.beers
        .filter(function(item)
          {    
            return item.name.toLowerCase().indexOf(vm.searchBeer.toLowerCase()) > -1
          })
        .sort((a,b) => {
          let modifier = 1;
          if(this.sortDirection === 'desc') modifier = -1;
          if(a[this.sortCat] < b[this.sortCat]) return -1 * modifier;
          if(a[this.sortCat] > b[this.sortCat]) return 1 * modifier;
          return 0;
        });
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import "@/assets/scss/mixins.scss";
table {
  font-family: 'Open Sans', sans-serif;
  width: 100%;
  border-collapse: collapse;
  border: 3px solid #44475C;
  margin: 20px auto;
  th {
    text-transform: uppercase;
    text-align: left;
    background: #44475C;
    color: #FFF;
    cursor: pointer;
    padding: 8px;
    min-width: 30px;
    &:hover {
        background: #717699;
    }
  }
  td {
      text-align: left;
      padding: 8px;
      border: 2px solid #7D82A8;
    }
  tr {
      border: 2px solid #7D82A8;
  }
  tbody tr:nth-child(2n) td {
      background: #D4D8F9;
  }
}
.add-beer {
    float:right;
    margin:20px 0;
}
.searchForm {
  float:left;
  margin: 20px 0;
  .search {
    position: relative;
    width:300px;
    @include border-radius(5px);
    border:1px solid #ddd;
    height:36px;
    margin-left: 10px;
    font-size: 16px;
    padding:5px 15px;
  }
  .add-beer {
    @include border-radius(5px);
    background: #eb5167;
    width:200px;
    height:40px;
    text-align:center;
    color:#fff;
  }
}
</style>
