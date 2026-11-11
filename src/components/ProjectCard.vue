<template>
    <div class="col-12 col-md-6 col-lg-4 mb-4">
        <div class="project-card h-100 shadow-sm border rounded overflow-hidden">
            <div class="project-image">
                <img :src="project.image" class="card-img-top" :alt="project.title" loading="lazy">
            </div>
            <div class="card-body text-start p-4">
                <span class="project-type text-muted small fw-bold">{{ project.type }}</span>
                <h2 class="card-title h4 mt-2">{{ project.title }}</h2>
                <p class="card-text text-secondary mt-3">
                    {{ project.description }}
                </p>
            </div>
        </div>
    </div>
</template>

<script setup>
import { defineProps } from "vue";

defineProps({
    project: {
        type: Object,
        required: true
    }
});
</script>