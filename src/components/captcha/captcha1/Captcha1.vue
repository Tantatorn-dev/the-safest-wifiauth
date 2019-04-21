<template>
  <v-layout>
    <v-flex xs12 sm6 offset-sm3>
      <v-card>
        <v-card-title primary-title>
          <v-card class="captcha-head">
            <h2 :v-bind="this.selected_search_key" class="captcha-head-text">
              Select all images with {{ selected_search_key }}
            </h2>
          </v-card>
        </v-card-title>
        <v-card-media>
          <v-container align-center justify-center fluid grid-list-xl>
            <v-layout row wrap>
              <v-flex v-for="(item, index) in url" :key="index" xs4>
                <transition name="fade">
                  <img
                    @click="getImage(index)"
                    :src="item"
                    :key="item"
                    class="image"
                    alt="loading"
                    width="100%"
                    height="100%"
                  />
                </transition>
              </v-flex>
            </v-layout>
          </v-container>
        </v-card-media>

        <v-card-actions>
          <v-btn icon @click="handleChangeWord"
            ><v-icon>autorenew</v-icon></v-btn
          >
          <v-spacer></v-spacer>
          <v-btn flat color="primary">Verify</v-btn>
        </v-card-actions>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
var keys = ["wine", "flower", "cat", "mountain"];
export default {
  name: "Captcha1",
  data() {
    let key = keys[Math.floor(Math.random() * keys.length)];
    return {
      search_keys: keys,
      selected_search_key: key,
      url: [
        "https://source.unsplash.com/random/500x500/?" + key + "?11",
        "https://source.unsplash.com/random/500x500/?" + key + "?2334324",
        "https://source.unsplash.com/random/500x500/?" + key + "?4443240",
        "https://source.unsplash.com/random/500x500/?" + key + "?23234",
        "https://source.unsplash.com/random/500x500/?" + key + "?3233240",
        "https://source.unsplash.com/random/500x500/?" + key + "?29953",
        "https://source.unsplash.com/random/500x500/?" + key + "?234325",
        "https://source.unsplash.com/random/500x500/?" + key + "?22343249",
        "https://source.unsplash.com/random/500x500/?" + key + "?554340"
      ]
    };
  },
  methods: {
    getImage: function(index) {
      this.$set(
        this.url,
        index,
        "https://source.unsplash.com/random/500x500/?" +
          this.selected_search_key +
          "?" +
          new Date().getTime()
      );
    },
    handleChangeWord: function() {
      this.selected_search_key = this.search_keys[
        Math.floor(Math.random() * this.search_keys.length)
      ];
      for (let i = 0; i < 9; i++) {
        this.getImage(i);
      }
    }
  }
};
</script>

<style scoped>
.captcha-head {
  width: 100%;
  background: #4990e2;
  color: white;
  height: 100px;
}

.image:hover {
  opacity: 0.5;
}

.fade-enter-active {
  transition: opacity 3s ease-in-out;
}

.fade-enter-to {
  opacity: 1;
}

.fade-enter {
  opacity: 0;
}

.captcha-head-text {
  padding: 15px;
}
</style>
