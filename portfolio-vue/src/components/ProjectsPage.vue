<template>
  <section class="projects-page">
    <div class="page-header">
      <h2>Projects</h2>
      <p>These are some recent projects. Click the button to view each website.</p>
    </div>

    <div class="projects-grid">
      <article class="project-card" v-for="project in projects" :key="project.title">
        <div class="project-image" :style="{ backgroundImage: `url(${project.image})` }"></div>
        <div class="project-body">
          <h3>{{ project.title }}</h3>
          <p>{{ project.description }}</p>
          <a :href="project.url" target="_blank" rel="noopener" class="project-link">
            Go to Website
          </a>
        </div>
      </article>
    </div>
  </section>
</template>

<script setup>
const projects = [
  {
    title: 'Blog with Admin Dashboard',
    description: 'A responsive blog platform featuring content publishing, article management, and an integrated admin dashboard for backend operations.',
    image: new URL('@/assets/images/serlinaweb.png', import.meta.url).href,
    url: 'https://serlinaweb.desmoco.com.tw/',
  },
  {
    title: 'Website Redesign',
    description: 'A complete redesign of the Serlina website to improve user experience and modernize the look and feel.',
    image: new URL('@/assets/images/serlina.png', import.meta.url).href,
    url: 'https://serlina.desmoco.com.tw/',
  },
  {
    title: 'Desmoco E-commerce Platform',
    description: 'A full redesign of the Desmoco E-commerce platform, enhancing user experience, visual design, and overall usability.',
    image: new URL('@/assets/images/desmoco.png', import.meta.url).href,
    url: 'https://desmoco.com.tw/',
  },
];
</script>

<style scoped>
.projects-page {
  padding: 4rem 1.5rem;
  max-width: 1200px;
  margin: 0 auto;
}

.page-header {
  text-align: center;
  margin-bottom: 2rem;
}

.page-header h2 {
  margin-bottom: 0.5rem;
  font-size: 2.25rem;
}

.page-header p {
  max-width: 640px;
  margin: 0 auto;
  color: #555;
}

.projects-grid {
  display: grid;
  gap: 1.5rem;
  grid-template-columns: repeat(3, minmax(0, 1fr));
}

.project-card {
  border-radius: 16px;
  overflow: hidden;
  background: white;
  box-shadow: 0 20px 45px rgba(0, 0, 0, 0.08);
  display: flex;
  flex-direction: column;
}

.project-image {
  min-height: 180px;
  background-size: cover;
  background-position: center;
}

.project-body {
  padding: 1.5rem;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  gap: 1rem;
  height: 100%;
}

.project-body h3 {
  margin: 0;
  font-size: 1.25rem;
}

.project-body p {
  margin: 0;
  color: #4c4c4c;
  line-height: 1.65;
  text-align: justify;
}

.project-link {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  background-color: #007bff;
  color: white;
  text-decoration: none;
  border-radius: 999px;
  font-weight: 600;
  transition: background-color 0.2s ease;
  @media (min-width: 375px) {
    padding: 0.85rem 1.2rem;
  }
}

.project-link:hover {
  background-color: #0056c1;
}

@media (max-width: 900px) {
  .projects-grid {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
}

@media (max-width: 640px) {
  .projects-page {
    padding: 2rem 1rem;
  }

  .projects-grid {
    grid-template-columns: 1fr;
  }
}
</style>
