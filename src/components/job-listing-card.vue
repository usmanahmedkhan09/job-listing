<template>
  <div class="jobsCard">
    <img :src="getImageUrl(job?.logo)" alt="" />
  </div>
</template>
<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  props: {
    job: {
      type: Object,
    },
  },
  setup() {
    const getImageUrl = (name: any) => {
      return new URL(`../assets/images/${name}.svg`, import.meta.url).href;
    };
    return { getImageUrl };
  },
});
</script>
