<script setup>
import { ref, computed, defineProps } from 'vue';

const props = defineProps({
    job: Object,
});

const showFullDescription = ref(false);

const toggleDescription = () => {
    showFullDescription.value = !showFullDescription.value; // Update value correctly
};

const truncatedDescription = computed(() => {
    let description = props.job.description;

    if (!showFullDescription.value) {
        return description.substring(0, 90) + '...'; // Return truncated description
    }

    return description; // Return full description when toggled
});
</script>

<template>
    <div class="bg-white rounded-2xl shadow-lg overflow-hidden relative transition-all duration-300 hover:shadow-xl">
        <div class="p-6">
            <div class="mb-6">
                <div class="text-gray-500 text-sm uppercase tracking-wide">{{ job.type }}</div>
                <h3 class="text-2xl font-semibold text-gray-800">{{ job.title }}</h3>
            </div>

            <div class="text-gray-600 mb-5 leading-relaxed">{{ truncatedDescription }}
                <span class="italic cursor-pointer hover:text-green-400" @click="toggleDescription">{{
                    showFullDescription ? "LESS" : 'MORE'
                    }}</span>
            </div>


            <h3 class="text-lg font-medium text-green-600 mb-2">{{ job.salary }} / Year</h3>

            <div class="border-t border-gray-200 my-5"></div>

            <div class="flex flex-col lg:flex-row justify-between items-center lg:items-start">
                <div class="text-orange-600 flex items-center mb-4 lg:mb-0">
                    <i class="fa-solid fa-location-dot text-xl mr-2"></i>
                    <span class="text-sm">{{ job.location }}</span>
                </div>
                <a :href="'/job/' + job.id"
                    class="inline-flex items-center bg-green-500 hover:bg-green-600 text-white px-5 py-2 rounded-lg text-sm font-medium shadow-sm transition-all duration-300 ease-in-out">
                    Read More
                </a>
            </div>
        </div>
    </div>

</template>



<style></style>