<script setup>
import { defineProps } from 'vue';
import JobListingItem from './JobListingItem.vue';
import jobdatas from '../jobs.json'
import { RouterLink } from 'vue-router';

import { ref } from 'vue';

defineProps({
    limitPost: {
        type: Number,
    },
    showButton: {
        type: Boolean,
        default: false,
    }
})

const jobs = ref(jobdatas)
</script>

<template>
    <section class="bg-green-50 px-4 py-10">
        <div class="container-xl lg:container m-auto">
            <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">
                Browse Jobs
            </h2>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                <!-- Iterate over jobs array -->
                <JobListingItem v-for="(job, index) in jobs.slice(0, limitPost || jobs.length)" :key="job.id || index"
                    :job="job" />
            </div>
        </div>
    </section>
    <section v-if='showButton' class='m-auto max-w-lg my-10 px-6'>
        <RouterLink to='/jobs' class='block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700'>
            View All Jobs
        </RouterLink>
    </section>
</template>