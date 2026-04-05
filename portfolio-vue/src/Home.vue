<script setup>
import { ref } from 'vue';
import Header from './components/Header.vue';
import Content from './components/Content.vue';
import ProjectsPage from './components/ProjectsPage.vue';

const tabs = ['Home', 'Projects'];
const activeTab = ref('Home');
</script>

<template>
    <header>
        <Header :tabs="tabs" :activeTab="activeTab" @tab-change="activeTab = $event" />
    </header>
    <main>
        <Content v-if="activeTab === 'Home'" />
        <ProjectsPage v-else-if="activeTab === 'Projects'" />
    </main>
</template>