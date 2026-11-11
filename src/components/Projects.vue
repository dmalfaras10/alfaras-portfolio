<template>
    <!-- Projects Section Start -->
    <section class="container text-center p-2 p-lg-5" id="projects">
        <!-- My Projects Heading -->
        <h1 class="pt-5" id="title">My Projects</h1>
        <p class="pt-3 pb-5">
            A collection of projects that showcase my experience in web development, design, and problem-solving. Each project reflects the skills and technologies I have applied to create functional and user-friendly solutions.
        </p>

        <!-- Loop through regular project groups (3 per row) -->
        <div 
            v-for="(group, index) in chunkedProjects" 
            :key="'project-row-' + index" 
            class="row justify-content-center my-4"
        >
            <ProjectCard 
                v-for="project in group" 
                :key="project.id" 
                :project="project"
            />
        </div>

        <!-- Capstone Section Heading -->
        <h1 class="pt-5" id="title">My Capstone</h1>
        <p class="pt-3 pb-5">
            My capstone project represents the application of the knowledge and skills I developed throughout my studies. It demonstrates my ability to plan, design, develop, and implement a complete solution to address a specific problem or need.
        </p>

        <!-- Loop through capstone project groups (3 per row) -->
        <div 
            v-for="(group, index) in chunkedCapstones" 
            :key="'capstone-row-' + index" 
            class="row justify-content-center my-4 p"
        >
            <ProjectCard 
                v-for="project in group" 
                :key="project.id" 
                :project="project"
            />
        </div>
    </section>
</template>

<script setup>
import { computed } from 'vue';
import ProjectCard from './ProjectCard.vue';

// Import data from your separate JSON files
import projects from '../data/projects.json';
import capstones from '../data/capstones.json';

const chunkSize = 3;

// Computed chunking logic for regular projects
const chunkedProjects = computed(() => {
    const chunks = [];
    for (let i = 0; i < projects.length; i += chunkSize) {
        chunks.push(projects.slice(i, i + chunkSize));
    }
    return chunks;
});

// Computed chunking logic for capstone projects
const chunkedCapstones = computed(() => {
    const chunks = [];
    for (let i = 0; i < capstones.length; i += chunkSize) {
        chunks.push(capstones.slice(i, i + chunkSize));
    }
    return chunks;
});
</script>