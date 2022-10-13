<template>
  <v-card class="flex d-flex flex-column" hover>
    <v-card-text class="text-right pb-0">
      <v-chip
        small
        label
        dark
        class="mr-auto"
        :color="statuslist[i.status].color"
      >
        {{ statuslist[i.status].name }}
      </v-chip>
    </v-card-text>
    <v-card-text class="pt-0">
      <h2 class="title" color="text--primary">{{ i.name }}</h2>
      <p>{{ i.desc }}</p>
      <v-chip
        :color="taglist[tag].color"
        outlined
        small
        class="mr-1"
        v-for="tag in i.tags"
        :key="tag"
      >
        <v-icon small left>mdi-{{ taglist[tag].icon }}</v-icon>
        {{ taglist[tag].name }}
      </v-chip>
    </v-card-text>
    <v-spacer />
    <v-divider />
    <v-card-actions>
      <v-tooltip bottom v-for="link in i.link" :key="link.url">
        <template v-slot:activator="{ on, attrs }">
          <v-btn
            icon
            v-on="on"
            v-bind="attrs"
            @click.stop="redirect_url(link.url)"
          >
            <v-icon>mdi-{{ link.icon }}</v-icon>
          </v-btn>
        </template>
        <span>{{ link.url.replace("https://", "") }}</span>
      </v-tooltip>
      <v-tooltip bottom v-if="i.link.length == 0">
        <template v-slot:activator="{ on, attrs }">
          <v-btn icon v-on="on" v-bind="attrs">
            <v-icon>mdi-null</v-icon>
          </v-btn>
        </template>
        <span>未有链接</span>
      </v-tooltip>
      <v-spacer />
      <span class="text--secondary">{{ i.start }}</span>
    </v-card-actions>
  </v-card>
</template>
<script>
import projects from "@/assets/projects.json";

export default {
  props: ["i"],
  data: () => ({
    taglist: projects.tags,
    statuslist: projects.status
  }),
  methods: {
    redirect_url(url) {
      window.location.href = url;
    }
  }
};
</script>
