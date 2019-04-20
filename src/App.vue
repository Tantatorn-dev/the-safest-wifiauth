<template>
  <v-app>
    <v-toolbar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>Vuetify</span>
        <span class="font-weight-light">MATERIAL DESIGN</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn
        flat
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
      >
        <span class="mr-2">Latest Release</span>
      </v-btn>
    </v-toolbar>

    <v-content>
      <Captcha2></Captcha2>
    </v-content>

    <v-dialog v-model="dialog" persistent>
      <v-card>
        <video id="myVideo" width="100%" style="max-height: 80vh;"></video>
        <v-card-actions>
          <v-spacer></v-spacer>
          <p v-if="time >= 0">กรุณารอ {{ time }}</p>
          <v-btn v-if="time < 0" color="green darken-1" flat @click="close()"
            >ข้าม</v-btn
          >
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-app>
</template>

<script>
import Captcha2 from "./components/captcha/captcha2/Captcha2";

var vids = [
  require("@/assets/Hackathon/Sekiro-op.mp4"),
  require("@/assets/Hackathon/TSOVER.mp4"),
  require("@/assets/Hackathon/Ricardo-milos-pillar-men-theme.mp4"),
  require("@/assets/Hackathon/Shopee.mp4"),
  require("@/assets/Hackathon/daikey.mp4"),
  require("@/assets/Hackathon/Euro.mp4"),
  require("@/assets/Hackathon/Frog.mp4"),
  require("@/assets/Hackathon/jo-ranger.mp4"),
  require("@/assets/Hackathon/kaiyang.mp4"),
  require("@/assets/Hackathon/kaokae.mp4"),
  require("@/assets/Hackathon/Luxmix.mp4"),
  require("@/assets/Hackathon/pukking.mp4"),
  require("@/assets/Hackathon/puthai.mp4"),
  require("@/assets/Hackathon/TeemoRemix.mp4")
];

export default {
  name: "App",
  components: {
    Captcha2
  },
  data() {
    return {
      dialog: true,
      time: 10
    };
  },
  mounted() {
    var vid = document.getElementById("myVideo");
    // vid.loop = true;
    vid.autoplay = true;
    vid.ontimeupdate = () => {
      this.time = Math.round(10 - vid.currentTime);
    };

    vid.onended = () => {
      var index = Math.floor(Math.random() * vids.length);
      vid.src = vids[index];
      vid.load();
    };

    var index = Math.floor(Math.random() * vids.length);
    vid.src = vids[index];
    vid.load();
  },
  methods: {
    close() {
      var vid = document.getElementById("myVideo");
      vid.pause();
      this.dialog = false;
    }
  }
};
</script>
