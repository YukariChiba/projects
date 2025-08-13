<template>
  <v-card class="flex d-flex flex-column" hover>
    <v-card-text class="text-right pb-0" style="margin-bottom: -20px">
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
      <h2 class="title mb-2" color="text--primary">
        {{ i.name }}
      </h2>
      <p>{{ i.desc }}</p>
      <div class="mt-2">
        <v-chip
          v-for="tag in i.tags"
          :key="tag"
          :color="taglist[tag].color"
          outlined
          small
          class="mr-2 mb-1"
          :prepend-icon="`mdi-${taglist[tag].icon}`"
        >
          {{ taglist[tag].name }}
        </v-chip>
      </div>
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
      <v-chip :text="i.start" class="text--secondary" label />
    </v-card-actions>
  </v-card>
</template>
<script setup>
import projects from "@/assets/projects.json";

defineProps(["i"]);

const taglist = projects.tags;
const statuslist = projects.status;

const redirect_url = (url) => {
  window.location.href = url;
};
</script>
