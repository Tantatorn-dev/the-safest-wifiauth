<template>
  <v-layout>
    <v-flex xs12 sm6 offset-sm3>
      <v-card>
        <v-card-title primary-title>
          <div style="width: 100%;">
            <h3 class="headline mb-0">เลือกส่วนที่มี {{ name }}</h3>
            <v-alert :value="num > 1" type="error">
              คุณเลือกไม่ครบ กรุณาลองใหม่
            </v-alert>
          </div>
        </v-card-title>

        <v-slide-x-transition leave-absolute>
          <v-container grid-list-xs fluid :key="num">
            <v-layout row wrap>
              <v-flex v-for="n in 16" :key="n" xs3>
                <v-card flat tile>
                  <v-img :src="picPart[n - 1]" contain @click="click(n - 1)">
                    <v-expand-transition>
                      <div
                        v-if="select[n - 1]"
                        class="d-flex transition-fast-in-fast-out orange darken-2 v-card--reveal display-4 white--text"
                        style="height: 100%;"
                      >
                        <v-icon dark right class="ma-0">check_circle</v-icon>
                      </div>
                    </v-expand-transition>
                  </v-img>
                </v-card>
              </v-flex>
            </v-layout>
          </v-container>
        </v-slide-x-transition>

        <v-card-actions>
          <v-btn flat color="orange" @click="random()">Continue</v-btn>
          <v-btn flat color="orange">Explore</v-btn>
        </v-card-actions>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
import picslist from "./picslist";
export default {
  name: "Captcha2",
  data() {
    return {
      name: null,
      pic: null,
      picPart: [],
      select: [],
      num: 0,
      lastIndex: null
    };
  },
  mounted() {
    this.random();
  },
  methods: {
    random() {
      this.num = 1;
      let all = [];
      picslist.forEach(namePic => {
        namePic.pics.forEach(pic => {
          all.push({ name: namePic.name, pic: pic });
        });
      });

      var randIndex = this.lastIndex;
      while (randIndex == this.lastIndex)
        randIndex = Math.floor(Math.random() * all.length);
      this.lastIndex = randIndex;

      this.name = all[randIndex].name;
      this.pic = all[randIndex].pic;

      var canvas1 = document.createElement("canvas");
      var ctx = canvas1.getContext("2d");

      var canvas2 = document.createElement("canvas");
      var ctx2 = canvas2.getContext("2d");

      var side = 4;

      var img = new Image();
      img.onload = () => {
        canvas1.width = img.width;
        canvas1.height = img.height;
        ctx.drawImage(img, 0, 0);

        canvas2.width = img.width / side;
        canvas2.height = img.height / side;

        var out = [];
        for (var i = 0; i < side * side; i++) {
          var cropImg = ctx.getImageData(
            canvas2.width * (i % side),
            canvas2.height * Math.floor(i / side),
            canvas2.width,
            canvas2.height
          );
          ctx2.putImageData(cropImg, 0, 0);
          out.push(canvas2.toDataURL("image/png"));
        }

        this.picPart = out;

        this.select.forEach((val, index) => {
          if (val) this.click(index);
        });

        this.num++;
        this.$vuetify.goTo(0);
      };
      img.src = this.pic;
    },
    click(i) {
      this.$set(this.select, i, !this.select[i]);
    }
  }
};
</script>

<style scoped>
.v-card--reveal {
  align-items: center;
  bottom: 0;
  justify-content: center;
  opacity: 0.7;
  position: absolute;
  width: 100%;
}
.bottom-gradient {
  background-color: rgba(0, 0, 0, 0.3);
}
</style>
