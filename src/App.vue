<template>
  <v-app>
    <v-container max-width="1400px">
      <v-card
        title="Yukari Chiba's Projects"
        subtitle="Yukari 的项目列表"
        prepend-avatar="/favicon.jpg"
        position="sticky"
        class="mb-4"
        style="overflow-y: scroll; position: sticky; top: 0px; z-index: 114514"
      >
        <template #append>
          <div class="d-flex align-center flex-wrap">
            <v-select
              v-model="groupMode"
              :items="groupOptions"
              label="分组方式"
              density="compact"
              variant="outlined"
              hide-details
              class="mr-4"
              style="min-width: 150px"
            />
            <v-switch
              v-model="showHidden"
              label="显示无效项目"
              color="error"
              density="compact"
              hide-details
              inset
            />
          </div>
        </template>
      </v-card>

      <template v-for="group in groupedProjects" :key="group.title">
        <v-row v-if="groupMode !== 'none'" class="ma-4">
          <v-col cols="12">
            <div class="d-flex align-center">
              <v-icon class="mr-2" size="large">{{
                group.icon || "mdi-folder"
              }}</v-icon>
              <h2 class="text-h5 font-weight-bold">{{ group.title }}</h2>
              <v-chip size="small" class="ml-2" variant="tonal">{{
                group.list.length
              }}</v-chip>
            </div>
            <v-divider class="mt-2" />
          </v-col>
        </v-row>

        <v-row class="ma-4">
          <v-col
            v-for="project in group.list"
            :key="project.name + group.title"
            cols="12"
            sm="6"
            md="6"
            lg="4"
            class="d-flex flex-column"
          >
            <ProjectCard :i="project" />
          </v-col>
        </v-row>
      </template>

      <v-row v-if="groupedProjects.length === 0" class="ma-4">
        <v-col class="text-center text-grey"> 没有找到符合条件的项目 </v-col>
      </v-row>
    </v-container>
  </v-app>
</template>

<script setup>
import { ref, computed } from "vue";
import projects_json from "@/assets/projects.json";
import ProjectCard from "@/components/ProjectCard.vue";

const rawProjects = projects_json.projects;
const meta = projects_json.meta;
const statusDef = projects_json.status;

const groupMode = ref("none"); // none, lang, topic, status, year
const showHidden = ref(false);

const groupOptions = [
  { title: "默认排序 (时间)", value: "none" },
  { title: "编程语言", value: "lang" },
  { title: "主题", value: "topic" },
  { title: "开始年份", value: "year" },
  { title: "维护状态", value: "status" },
];

const groupedProjects = computed(() => {
  let list = rawProjects.filter(
    (p) =>
      showHidden.value ||
      (p.status !== "deprecated" &&
        p.status !== "abandoned" &&
        p.status !== "not-maintaining"),
  );

  const sortByDate = (a, b) => {
    const da = new Date(a.start.replace(".", "-"));
    const db = new Date(b.start.replace(".", "-"));
    return db - da;
  };

  list.sort(sortByDate);

  if (groupMode.value === "none") {
    return [{ title: "All", list: list, icon: "mdi-apps" }];
  }

  const groups = {};

  if (groupMode.value === "year") {
    list.forEach((p) => {
      const year = p.start.substring(0, 4);
      if (!groups[year]) groups[year] = [];
      groups[year].push(p);
    });
    return Object.keys(groups)
      .sort((a, b) => b - a)
      .map((year) => ({
        title: year,
        list: groups[year],
        icon: "mdi-calendar-clock",
      }));
  }

  if (groupMode.value === "status") {
    list.forEach((p) => {
      const s = p.status;
      if (!groups[s]) groups[s] = [];
      groups[s].push(p);
    });
    return Object.keys(groups).map((s) => ({
      title: statusDef[s]?.name || s,
      list: groups[s],
      icon: "mdi-list-status",
    }));
  }

  if (groupMode.value === "lang" || groupMode.value === "topic") {
    list.forEach((p) => {
      const keys = p[groupMode.value];
      if (!keys || keys.length === 0) {
        if (!groups["Other"]) groups["Other"] = [];
        groups["Other"].push(p);
      } else {
        keys.forEach((k) => {
          if (!groups[k]) groups[k] = [];
          groups[k].push(p);
        });
      }
    });

    return Object.keys(groups)
      .sort()
      .map((k) => ({
        title: meta[k]?.name || k,
        list: groups[k],
        icon: meta[k]?.icon ? `mdi-${meta[k].icon}` : "mdi-label",
      }));
  }

  return [];
});
</script>
