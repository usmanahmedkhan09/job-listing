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
          @input="debounceOnInput(searchJobs)"
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
    </div>
  </header>
  <main class="content">
    <jobListingCardVue
      v-for="(item, index) in filteredJobs"
      :key="index"
      :job="item"
      @filterJobs="(value) => filterJobs(value)"
    />
  </main>
</template>
<script lang="ts">
import { defineComponent, ref, computed } from "vue";
import jobListingCardVue from "@/components/job-listing-card.vue";
import jobsData from "../assets/data.json";

export default defineComponent({
  components: { jobListingCardVue },
  setup() {
    const jobs = ref(jobsData);

    const input = ref();

    let keyword = ref("");

    let timeout = ref();

    let selectfilters = ref<any[]>([]);

    const filteredJobs = computed(() => {
      if (selectfilters.value.length > 0) {
        return jobs.value.filter((x: any) => {
          if (
            selectfilters.value.includes(x.role) ||
            selectfilters.value.includes(x.level) ||
            x.tools.some((item: any) => selectfilters.value.includes(item)) ||
            x.languages.some((item: any) => selectfilters.value.includes(item))
          ) {
            return x;
          }
        });
      } else {
        return jobs.value;
      }
    });

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
        filterJobs();
      } else {
        selectfilters.value = [];
      }
    };

    const debounceOnInput = (func: any, ms: number = 1000) => {
      clearTimeout(timeout.value);
      timeout.value = setTimeout(() => func(), ms);
    };

    const searchJobs = () => {
      jobs.value = jobs.value.filter((x: any) => {
        if (
          x.tools.some(
            (item: any) => item.toLowerCase() == keyword.value.toLowerCase()
          ) ||
          x.languages.some(
            (item: any) => item.toLowerCase() == keyword.value.toLowerCase()
          ) ||
          x.role.toLowerCase() == keyword.value.toLowerCase() ||
          x.level.toLowerCase() == keyword.value.toLowerCase()
        ) {
          return x;
        }
      });
    };

    const filterJobs = (payload: any = null) => {
      if (payload) {
        selectfilters.value.push(payload);
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
      searchJobs,
      timeout,
      debounceOnInput,
      filterJobs,
      filteredJobs,
    };
  },
});
</script>
