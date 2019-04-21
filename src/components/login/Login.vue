<template>
  <v-container fluid fill-height>
    <v-layout justify-center>
      <v-flex xs12 sm12 md5>
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
export default {
  name: "Login",
  components: {
    Captcha1,
    Captcha2
  },
  data() {
    return {
      dialog: false
    };
  }
};
</script>
