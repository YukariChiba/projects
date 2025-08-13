<template>
  <v-app>
    <v-container max-width="1400px">
      <v-card
        title="Yukari Chiba's Projects"
        subtitle="Yukari 的项目列表"
        prepend-avatar="/favicon.jpg"
        position="sticky"
        style="overflow-y: scroll; position: sticky; top: 0px; z-index: 114514"
      />
      <v-row class="ma-4">
        <v-col
          v-for="i in projects"
          :key="i.name"
          cols="12"
          sm="6"
          md="6"
          lg="4"
          class="d-flex flex-column"
        >
          <ProjectCard :i="i" />
        </v-col>
      </v-row>
    </v-container>
  </v-app>
</template>

<script setup>
import projects_json from "@/assets/projects.json";
import ProjectCard from "@/components/ProjectCard.vue";

const projects = projects_json.projects;
</script>
