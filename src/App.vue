<template>
  <div id="app">
    <b-navbar toggleable="lg" type="dark" variant="primary" class="fixed-top">
      <b-navbar-brand>
        <img src="../images/dictionary.png" alt="">
        <span> UrbanDictionary</span>
        </b-navbar-brand>
      <b-navbar-nav class="ml-auto">
          <b-form-input size="bg" class="mr-sm-2" placeholder="Search" v-model="search" @keyup.enter="SearchWord" ></b-form-input>
          <b-button size="sm" class="my-2 my-sm-0 btn-success" @click="SearchWord">Search</b-button>
      </b-navbar-nav>
    </b-navbar>
    <div class="container">
      <div class="" v-if="podaci">
        <post-container-vue  v-for="item in podaci" :key="item.defid" :post="item"></post-container-vue>
      </div>
    </div>
    <b-navbar toggleable="lg" type="dark" variant="secondary" :class="podaci? 'sticky-bottom':'fixed-bottom'">
      <b-navbar-brand href="#">
        <img src="../images/dictionary.png" alt="">
        <span> UrbanDictionary</span>
      </b-navbar-brand>
      <b-nav-text>
        Copyright &copy;2019 by WickeD
      </b-nav-text>
    </b-navbar>
  </div>
</template>

<script>
import PostContainerVue from './components/PostContainer.vue';

export default {
  name: 'app',
  components: {
    PostContainerVue
  },
  data: function() {
    return {
      podaci: "",
      search:"",
    };
  },
  methods:{
    SearchWord:function(){
      fetch(`https://mashape-community-urban-dictionary.p.rapidapi.com/define?term=${this.search}`, {
        "method": "GET",
        "headers": {
          "x-rapidapi-host": "mashape-community-urban-dictionary.p.rapidapi.com",
          "x-rapidapi-key": "3ad5e9566emsh12b9dd01eb2e595p10f4e7jsnca728172e1ea"
        }
      })
      .then(response => {
        return response.json();
      })
      .then(JSONdata=>{
        this.podaci=JSONdata.list;
      })
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin-top: 60px;
}
</style>
