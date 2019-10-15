<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'app',
  components: {
    HelloWorld
  },
  data: function() {
    return {
      podaci: "The only [proper] [response] to something that makes absolutely [no sense].",
      result:"",
      podacilink:""
    };
  },
  methods:{
    toLink:function(){
      var patt = /\[(.*?)\]/g;
      var result = this.podaci.match(patt);
      this.result=result;
      var prefix = "<a href='";
      var mid = "'>";
      var sufix = "</a>";
      var link="";
      var links=[];
      for(let i=0;i<result.length;i++)
      {
        result[i]=result[i].slice(1,result[i].length-1);
        links.push(prefix+link+mid+result[i]+sufix);
      }
      for(let i=0;i<links.length;i++)
      {
        let tmpPodaci = this.podaci.replace(/\[(.*?)\]/, links[i]);
        this.podaci = tmpPodaci;
      }
    }
  },
  mounted() {
    fetch(
      "https://andruxnet-random-famous-quotes.p.rapidapi.com/?cat=movies&count=10",
      {
        method: "GET",
        headers: {
          "x-rapidapi-host": "andruxnet-random-famous-quotes.p.rapidapi.com",
          "x-rapidapi-key": "3ad5e9566emsh12b9dd01eb2e595p10f4e7jsnca728172e1ea"
        }
      }
    )
      .then(response => response.json())
      .then(jsonData => {
        this.podaci = jsonData;
      });
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
