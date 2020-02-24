<template>
  <v-col cols="12" class="d-lg-none">
    <v-card class="navdrawer" dark>
      <v-card-title>
        0x7f Projects
      </v-card-title>
      <v-card-subtitle>
        Charles 的项目列表
      </v-card-subtitle>
      <v-card-actions>
        <v-spacer />
        <v-btn
          icon
          @click.stop="redirect_url('https://github.com/SteveCharlesYang')"
          ><v-icon>mdi-git</v-icon></v-btn
        >
        <v-btn icon @click.stop="redirect_url('https://t.me/CharlesYang')"
          ><v-icon>mdi-telegram</v-icon></v-btn
        >
        <v-btn icon @click.stop="redirect_url('https://0x7f.cc')"
          ><v-icon>mdi-web</v-icon></v-btn
        >
        <v-btn icon @click.stop="redirect_url('mailto:Charles@0x7f.cc')"
          ><v-icon>mdi-email</v-icon></v-btn
        >
      </v-card-actions>
    </v-card>
  </v-col>
</template>
