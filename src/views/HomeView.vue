<template>
  <header class="header">
    <!-- <div class="header__autocomplete" contenteditable="true"></div> -->
  </header>
  <main class="content">
    <jobListingCardVue v-for="item in [1, 2, 3, 4, 4]" :key="item" />
  </main>
</template>
<script lang="ts">
import { defineComponent } from "vue";
import jobListingCardVue from "@/components/job-listing-card.vue";

export default defineComponent({
  components: { jobListingCardVue },
  setup() {
    return {};
  },
});
</script>
