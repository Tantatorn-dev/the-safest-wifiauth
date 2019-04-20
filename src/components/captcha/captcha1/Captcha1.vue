<template>
  <v-layout>
    <v-flex xs12 sm6 offset-sm3>
      <v-card>
        
        <v-card-title primary-title>
            <v-card class="captcha-head">
              <h1>Select all images with Pepsi logo</h1>
            </v-card>
        </v-card-title>

        <v-card-media>
           <v-container align-center justify-center fluid grid-list-xl>
              <v-layout row wrap>
              <v-flex v-for="(item,index) in url" :key="index" xs4>
                <img  @click="getImage(index)" :src="item" class="image" alt="lorem" width="100%" height="100%">
              </v-flex>
              </v-layout>
            </v-container>
        </v-card-media>

        <v-card-actions>
          <v-btn flat color="primary">Verify</v-btn>
        </v-card-actions>

      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
export default {
    name: "Captcha1",
    data(){
      return{
        search_keys:["hamburger","hotdog","fruit","beer","wine",
                    "bird","cheese","tree"],
        url:["https://source.unsplash.com/random/500x500/?fruit?11"
        ,"https://source.unsplash.com/random/500x500/?fruit?2334324"
        ,"https://source.unsplash.com/random/500x500/?fruit?4443240"
        ,"https://source.unsplash.com/random/500x500/?fruit?23234"
        ,"https://source.unsplash.com/random/500x500/?fruit?3233240"
        ,"https://source.unsplash.com/random/500x500/?fruit?29953"
        ,"https://source.unsplash.com/random/500x500/?fruit?234325"
        ,"https://source.unsplash.com/random/500x500/?fruit?22343249"
        ,"https://source.unsplash.com/random/500x500/?fruit?554340"
        ]
      }
    },
    methods:{
      getImage:function(index){
        console.log(index)
        this.$set(this.url,index,"https://source.unsplash.com/random/500x500/?fruit?"+new Date().getTime())
      }
    }
}
</script>

<style scoped>
.captcha-head{
  width:100%;
  background: #4990e2;
  color:white;
}
.image:hover{
  opacity: 0.5;
}
</style>
