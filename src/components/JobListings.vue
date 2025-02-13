<script setup>
import axios from "axios";
import JobListing from "./JobListing.vue";
import { onMounted, reactive } from "vue";
import { RouterLink } from "vue-router";
import { Loader2 } from "lucide-vue-next";
const state = reactive({
  jobs: [],
  isLoading: true,
});
defineProps({
  limit: Number,
  showButton: {
    type: Boolean,
    default: false,
  },
});
onMounted(async () => {
  try {
    const response = await axios.get("/api/jobs");
    state.jobs = response.data;
  } catch (error) {
    console.error("Error fetching jobs", error);
  } finally {
    state.isLoading = false;
  }
});
</script>

<template>
  <section class="bg-blue-50 px-4 py-10">
    <div class="container-xl lg:container mx-auto">
      <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">
        Browse Jobs
      </h2>
      <div v-if="state.isLoading" class="h-40">
        <Loader2 class="animate-spin mt-5 mx-auto size-30 text-green-700" />
      </div>
      <div v-else class="grid grid-cols-1 gap-6 md:grid-cols-3 items-start">
        <JobListing
          v-for="job in state.jobs.slice(0, limit ?? state.jobs.length)"
          :key="job.id"
          :job="job"
        />
      </div>
    </div>
  </section>
  <section v-if="showButton" class="m-auto max-w-lg my-10 px-6">
    <RouterLink
      to="/jobs"
      class="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700"
      >View All Jobs</RouterLink
    >
  </section>
</template>
