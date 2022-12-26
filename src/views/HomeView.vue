<template>
  <header class="header">
    <!-- <div class="header__autocomplete" contenteditable="true"></div> -->
  </header>
  <main class="content">
    <jobListingCardVue v-for="(item, index) in jobs" :key="index" :job="item" />
  </main>
</template>
<script lang="ts">
import { defineComponent, ref } from "vue";
import jobListingCardVue from "@/components/job-listing-card.vue";
import jobsData from "../assets/data.json";

export default defineComponent({
  components: { jobListingCardVue },
  setup() {
    const jobs = ref(jobsData);
    return { jobs };
  },
});
</script>
