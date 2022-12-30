<template>
  <header class="header">
    <div class="header__autocomplete">
      <div class="header__autocomplete--filtersWrapper">
        <div
          class="header__autocomplete--filters"
          v-for="(item, index) in selectfilters"
          :key="index"
        >
          <span class="keyword">{{ item }}</span>
          <div class="icon" @click="clearFilter(item)">
            <img src="../assets/images/icon-remove.svg" alt="" />
          </div>
        </div>
        <input
          v-model="keyword"
          class="input"
          type="text"
          @keypress.enter="handleKeyword($event)"
        />
      </div>

      <p
        v-if="selectfilters.length > 0"
        @click="clearFilter()"
        class="clear"
        href="#"
      >
        Clear
      </p>
      <!-- <div
        ref="input"
        class="input"
        contenteditable="true"
        @keypress.enter="handleKeyword($event)"
        @input="updateInput($event)"
      ></div> -->
    </div>
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

    const input = ref();

    let keyword = ref("");

    let selectfilters = ref<any[]>([]);

    const updateInput = (e: any) => {
      keyword.value = e.target.innerText;
    };

    const handleKeyword = (e: any) => {
      selectfilters.value.push(keyword.value);
      keyword.value = "";
    };

    const clearFilter = (value: string = "") => {
      if (value) {
        selectfilters.value = selectfilters.value.filter(
          (item: any) => item != value
        );
      } else {
        selectfilters.value = [];
      }
    };
    return {
      jobs,
      handleKeyword,
      updateInput,
      selectfilters,
      input,
      keyword,
      clearFilter,
    };
  },
});
</script>
