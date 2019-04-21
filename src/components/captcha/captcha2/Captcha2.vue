<template>
  <v-layout>
    <v-flex xs12 sm6 offset-sm3>
      <v-card>
        <v-card-title primary-title>
          <div style="width: 100%;">
            <h3 class="headline mb-0">เลือกส่วนที่มี {{ name }}</h3>
            <v-alert
              :value="state >= 2 && state != 10"
              type="error"
              class="pa-2"
            >
              คุณเลือกคำตอบที่ถูกต้องไม่ครบ กรุณาลองใหม่
            </v-alert>
            <v-alert :value="state == 10" type="error" class="pa-2">
              กรุณาเลือกอย่างน้อยหนึ่งช่อง
            </v-alert>
          </div>
        </v-card-title>

        <v-slide-x-transition leave-absolute>
          <v-container grid-list-xs fluid :key="state">
            <v-img :src="pic" contain>
              <table>
                <tr v-for="i in 4" :key="i">
                  <td v-for="j in 4" :key="j">
                    <div
                      @click="click((i - 1) * 4 + j - 1)"
                      style="height: 100%; width: 100%;"
                    >
                      <v-fade-transition>
                        <div
                          v-if="select[(i - 1) * 4 + j - 1]"
                          class="d-flex transition-fast-in-fast-out v-card--reveal display-4"
                          :style="{
                            height: '25%',
                            width: '25%',
                            top: (i - 1) * 25 + '%',
                            left: (j - 1) * 25 + '%'
                          }"
                        >
                          <v-icon right class="ma-0" style="color: black;"
                            >check_circle</v-icon
                          >
                        </div>
                      </v-fade-transition>
                    </div>
                  </td>
                </tr>
              </table>
            </v-img>
          </v-container>
        </v-slide-x-transition>

        <v-card-actions>
          <v-btn flat color="primary" @click="skip()">ข้าม</v-btn>
          <v-spacer />
          <v-btn color="primary" @click="check()"
            >ต่อไป<v-icon dark right>arrow_forward</v-icon></v-btn
          >
        </v-card-actions>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
import picslist from "./picslist";

var all = [];
picslist.forEach(namePic => {
  namePic.pics.forEach(pic => {
    all.push({ name: namePic.name, pic: pic });
  });
});

export default {
  name: "Captcha2",
  data() {
    return {
      name: null,
      pic: "",
      picPart: [],
      select: [],
      state: 0,
      lastIndex: null
    };
  },
  mounted() {
    for (var i = 0; i < 16; i++) this.select.push(false);
    this.random();
  },
  methods: {
    skip() {
      this.state = 0;
      this.random();
    },
    check() {
      if (!this.select.some(val => val)) {
        this.state = 10;
        this.$vuetify.goTo(0);
      } else this.random();
    },
    random() {
      var randIndex = this.lastIndex;
      while (randIndex == this.lastIndex)
        randIndex = Math.floor(Math.random() * all.length);
      this.lastIndex = randIndex;

      this.name = all[randIndex].name;
      this.pic = all[randIndex].pic;

      for (var i = 0; i < this.select.length; i++) this.select[i] = false;

      this.state++;
      if (this.state > 9) this.state = 2;
      this.$vuetify.goTo(0);
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
  position: absolute;
  width: 100%;
  background-color: rgb(255, 255, 255, 0.6);
}
table {
  table-layout: fixed;
  width: 100%;
  height: 100%;
  border-collapse: collapse;
  border-style: hidden;
}
th,
tr,
td {
  width: 25%;
  border-style: solid;
  border-color: white;
}
</style>
