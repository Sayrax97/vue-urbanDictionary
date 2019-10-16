<template>
  <div class="container ">
      <div class="row">
          <a class="font-weight-bold text-monospace h2" :href="post.permalink" target="_blank">{{post.word}}</a>
      </div>
      <div class="row">
          {{toLink(post.definition)}}
      </div>
      <div class="row">
          {{toLink(post.example)}}
      </div>
      <div class="row">
          <div class="col-md-auto">
            <b-button-group>
                <b-button variant="success"><img src="../../images/like.png" alt="upvote"><span>{{post.thumbs_up}}</span></b-button>
                <b-button variant="danger"><img src="../../images/dislike.png" alt="downvote"><span>{{post.thumbs_down}}</span></b-button>
            </b-button-group>
          </div>
          <div class="col-md">  
              <p class="text-center">by {{post.author}}--{{convertDate(post.written_on)}}</p>
          </div>
      </div>
      <div class="row">
        <div class="col" v-for="audio in post.sound_urls" :key="audio">
            <audio  controls>
              <source :src="audio" type="audio/wav">
            </audio>
        </div>
      </div>
  </div>
</template>

<script>
export default {
    props:{
        post:Object
    },
    methods:{
    toLink:function(d){
      var patt = /\[(.*?)\]/g;
      var result = d.match(patt);
      var prefix = "<a href=''";
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
        let tmpPodaci = d.replace(/\[(.*?)\]/, links[i]);
        d = tmpPodaci;
      }
      return d;
    },
    convertDate(date){
        var dt=new Date(date);
        return dt.toDateString();
    }
  }

}
</script>

<style scoped>

</style>