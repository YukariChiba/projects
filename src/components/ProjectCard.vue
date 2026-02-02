<template>
  <v-card class="flex d-flex flex-column h-100" hover>
    <v-card-text class="text-right pb-0" style="margin-bottom: -20px">
      <v-chip
        size="small"
        label
        dark
        class="mr-auto"
        :color="statuslist[i.status]?.color || 'grey'"
      >
        {{ statuslist[i.status]?.name || i.status }}
      </v-chip>
    </v-card-text>
    <v-card-text class="pt-0">
      <h2 class="text-h6 mb-2 font-weight-bold">
        {{ i.name }}
      </h2>
      <p class="text-body-2">{{ i.desc }}</p>
      <div class="mt-2">
        <template v-for="tagKey in displayTags" :key="tagKey">
          <v-chip
            v-if="meta[tagKey]"
            :color="meta[tagKey].color"
            variant="outlined"
            size="small"
            class="mr-2 mb-1"
            :prepend-icon="`mdi-${meta[tagKey].icon}`"
          >
            {{ meta[tagKey].name }}
          </v-chip>
          <v-chip
            v-else
            color="grey"
            variant="outlined"
            size="small"
            class="mr-2 mb-1"
            prepend-icon="mdi-label"
          >
            {{ tagKey }}
          </v-chip>
        </template>
      </div>
    </v-card-text>
    <v-spacer />
    <v-divider />
    <v-card-actions>
      <template v-for="link in i.link" :key="link.url">
        <v-tooltip location="bottom">
          <template #activator="{ props }">
            <v-btn
              icon
              v-bind="props"
              variant="text"
              @click.stop="open_url(link.url)"
            >
              <v-icon>mdi-{{ link.icon }}</v-icon>
            </v-btn>
          </template>
          <span>{{ link.url.replace("https://", "") }}</span>
        </v-tooltip>
      </template>

      <v-tooltip location="bottom" v-if="!i.link || i.link.length == 0">
        <template v-slot:activator="{ props }">
          <v-btn icon v-bind="props" variant="text" disabled>
            <v-icon>mdi-link-off</v-icon>
          </v-btn>
        </template>
        <span>未有链接</span>
      </v-tooltip>
      <v-spacer />
      <v-chip size="small" label class="text-secondary">
        {{ i.start }}
      </v-chip>
    </v-card-actions>
  </v-card>
</template>

<script setup>
import { computed } from "vue";
import projects from "@/assets/projects.json";

const props = defineProps(["i"]);

const meta = projects.meta;
const statuslist = projects.status;

const displayTags = computed(() => {
  const langs = props.i.lang || [];
  const topics = props.i.topic || [];
  return [...langs, ...topics];
});

const open_url = (url) => {
  window.open(url, "_blank");
};
</script>
