<script setup>
import { ArrowLeft } from 'lucide-vue-next';
import { RouterLink } from 'vue-router';

</script>

<template>
     <section>
      <div class="container mx-auto p-6">
        <RouterLink
          to="/jobs"
          class="text-green-500 hover:text-green-600 flex items-center"
        >
          <ArrowLeft class="inline size-4 mr-2"/> Back to Job Listings
        </RouterLink>
      </div>
    </section>
</template>