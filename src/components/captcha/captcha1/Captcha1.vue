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
              <v-flex v-for="i in num" :key="i" xs4>
                <img  :src="`https://randomuser.me/api/portraits/men/${i + 20}.jpg`" class="image" alt="lorem" width="100%" height="100%">
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
