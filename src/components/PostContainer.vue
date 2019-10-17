<template>
  <div class="postStyle border border-secondary rounded container">
      <div class="row">
          <a class="font-weight-bold text-monospace h2" :href="post.permalink" target="_blank">{{post.word}}</a>
          <button v-if="post.sound_urls" class=" rounded-circle btn" @click.prevent="playSound(post.sound_urls[0])">
          <img src="../../images/play-button.png" alt="">
          </button>
      </div>
      <div class="row definition font-weight-bolder " >
        <p v-html="toLink(post.definition)">
        </p>
      </div>
      <div class="row example" >
        <p v-html="toLink(post.example)">
        </p>
      </div>
      <div class="row author">
          <div class="col-md-auto">
            <b-button-group class="ml-auto ">
                <b-button variant="success" @click="upvote"><img src="../../images/like.png" alt="upvote"><span>{{post.thumbs_up}}</span></b-button>
                <b-button variant="danger"  @click="downvote"><img src="../../images/dislike.png" alt="downvote"><span>{{post.thumbs_down}}</span></b-button>
            </b-button-group>
          </div>
          <div class="col-md">  
              <p class="text-center">by {{post.author}}--{{convertDate(post.written_on)}}</p>
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
      var prefix = "<a href='";
      var mid = "' onclick='clickedLink(this)'>";
      var sufix = "</a>";
      var link="#";
      var links=[];
      for(let i=0;i<result.length;i++)
      {
        result[i]=result[i].slice(1,result[i].length-1);
        links.push(" "+prefix+link+mid+result[i]+sufix+" ");
      }
      for(let i=0;i<links.length;i++)
      {
        let tmpPodaci = d.replace(/\[(.*?)\]/, links[i]);
        d = tmpPodaci;
      }
      return d;
    },
    clickedLink:function(link){
      event.preventDefault
      alert(link.innerHTML);
    },
    convertDate(date){
        var dt=new Date(date);
        return dt.toDateString();
    },
    upvote(){
      this.post.thumbs_up++;
    },
    downvote(){
      this.post.thumbs_down++;
    },
    playSound (sound) {
      if(sound) {
        var audio = new Audio(sound);
        audio.play();
      }
    }
  }

}
</script>

<style scoped>
.postStyle{
  margin-top: 5px;
  margin-bottom: 5px;
}
.definition{
  margin-left: 10px;
  padding: 5px;
}
.example{
  margin-left: 10px;
  padding: 5px;
}
.author{
  margin: 5px;
}
</style>