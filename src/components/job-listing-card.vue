<template>
  <div class="jobsCard">
    <div class="jobsCard__image">
      <img class="" :src="getImageUrl(job?.logo)" alt="" />
    </div>
    <div class="jobsCard__des">
      <p class="title">
        {{ job?.company }} <span class="new" v-if="job?.new">NEW!</span>
        <span class="feature" v-if="job?.featured">featured</span>
      </p>
      <p class="position">{{ job?.position }}</p>
      <ul class="list">
        <li>{{ job?.postedAt }}</li>
        <li>{{ job?.contract }}</li>
        <li>{{ job?.location }}</li>
      </ul>
    </div>
    <ul class="jobsCard__tools">
      <li>{{ job?.role }}</li>
      <li>{{ job?.level }}</li>
      <li v-for="(language, index) in job?.languages" :key="index">
        {{ language }}
      </li>
      <li v-for="(tool, index) in job?.tools" :key="index">
        {{ tool }}
      </li>
    </ul>
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
