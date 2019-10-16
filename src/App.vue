<template>
  <div id="app">
      <div class="container">
        <div class="row">
          <div class="col-lg">
            <b-form-input size="bg" class="mr-sm-2" placeholder="Search" v-model="search"></b-form-input>
          </div>
          <div>
            <b-button size="bg"  @click="SearchWord">Search</b-button>
          </div>
        </div>
      </div>
    <div v-if="podaci">
    <post-container-vue  v-for="item in podaci" :key="item.defid" :post="item"></post-container-vue>
    </div>
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
      search:""
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
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
