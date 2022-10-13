<template>
  <v-app>
    <NavDrawer />
    <v-content>
      <v-container>
        <v-row class="ma-4">
          <MobileNav />
          <v-col
            cols="12"
            sm="6"
            md="6"
            lg="4"
            v-for="i in projects"
            :key="i.name"
            class="d-flex flex-column"
          >
            <ProjectCard :i="i" />
          </v-col>
        </v-row>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import projects from "@/assets/projects.json";
import NavDrawer from "@/components/NavDrawer.vue";
import ProjectCard from "@/components/ProjectCard.vue";
import MobileNav from "@/components/MobileNav.vue";

export default {
  name: "App",

  data: () => ({
    projects: projects.projects,
    taglist: projects.tags
  }),
  components: {
    NavDrawer,
    ProjectCard,
    MobileNav
  }
};
</script>
<style lang="scss">
.navdrawer {
  background: linear-gradient(#e769e0, darken(#8aabff, 5%));
}
</style>
