<template>
  <v-navigation-drawer app class="navdrawer" dark>
    <v-container fill-height>
      <v-row justify="center" align="center">
        <v-avatar size="96" v-ripple v-on="on">
          <v-img src="@/assets/icon.jpg" />
        </v-avatar>
        <v-col cols="12">
          <v-card-title class="white--text justify-center">
            0x7f Projects
          </v-card-title>
          <v-card-subtitle class="white--text text-center">
            Yukari 的项目列表
          </v-card-subtitle>
          <v-card-actions class="justify-center">
            <v-btn
              icon
              @click.stop="redirect_url('https://github.com/YukariChiba')"
              ><v-icon>mdi-git</v-icon></v-btn
            >
            <v-btn icon @click.stop="redirect_url('https://t.me/CharlesYang')"
              ><v-icon>mdi-telegram</v-icon></v-btn
            >
            <v-btn icon @click.stop="redirect_url('https://0x7f.cc')"
              ><v-icon>mdi-web</v-icon></v-btn
            >
            <v-btn icon @click.stop="redirect_url('mailto:i@0x7f.cc')"
              ><v-icon>mdi-email</v-icon></v-btn
            >
          </v-card-actions>
        </v-col>
      </v-row>
    </v-container>
  </v-navigation-drawer>
</template>
<script>
export default {
  methods: {
    redirect_url(url) {
      window.location.href = url;
    }
  }
};
</script>
