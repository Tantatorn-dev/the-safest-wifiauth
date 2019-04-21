<template>
  <v-container fluid fill-height grid-list-md text-xs-center>
    <v-layout justify-center row wrap>
      <v-flex xs12 sm12 md6>
        <v-card class="elevation-12">
          <v-toolbar dark color="primary">
            <v-toolbar-title
              >Please log on to use the internet hotspot
              service</v-toolbar-title
            >
          </v-toolbar>
          <v-card-text>
            <v-form>
              <v-text-field
                prepend-icon="person"
                name="login"
                label="Login"
                type="text"
              ></v-text-field>
              <v-text-field
                prepend-icon="lock"
                name="password"
                label="Password"
                id="password"
                type="password"
              ></v-text-field>
            </v-form>
          </v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="primary" @click="dialog = true">Login</v-btn>
          </v-card-actions>
        </v-card>
      </v-flex>

      <v-flex v-for="(spon, index) in sponsor" :key="index" xs3 sm2>
        <v-card>
          <v-img :src="spon" contain />
        </v-card>
      </v-flex>
    </v-layout>
    <v-dialog
      v-model="dialog"
      fullscreen
      hide-overlay
      transition="dialog-bottom-transition"
    >
      <Captcha1></Captcha1>
    </v-dialog>
  </v-container>
</template>

<script>
import Captcha1 from "../captcha/captcha1/Captcha1";
import Captcha2 from "../captcha/captcha2/Captcha2";

var sponsor = [
  require("@/assets/sponsor/fastwork.jpg"),
  require("@/assets/sponsor/Kulap.png"),
  require("@/assets/sponsor/React.png"),
  require("@/assets/sponsor/siam.png"),
  require("@/assets/sponsor/taskworld_logo.png"),
  require("@/assets/sponsor/ThoughtWorks-Alta.jpg"),
  require("@/assets/sponsor/wise-sight.jpg")
];
export default {
  name: "Login",
  components: {
    Captcha1,
    Captcha2
  },
  data() {
    return {
      dialog: false,
      sponsor
    };
  }
};
</script>
