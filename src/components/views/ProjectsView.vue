<template>
  <section id="projects">
    <div class="container appear-on-scroll">
      <h2>{{ $t('PROJECTS.TITLE') }}</h2>

      <div class="featured-project-cards">
        <FeaturedProjectCard
          v-for="(project, index) in featuredProjects"
          :key="index"
          :project="project"
          :reverse="index % 2 === 0"
        />
      </div>

      <div class="project-cards">
        <ProjectCard
          v-for="(project, index) in projects"
          :key="index"
          :project="project"
        />
      </div>

      <div class="coming-soon-message">
        <h1>{{ $t('PROJECTS.COMING_SOON')}}</h1>
      </div>
    </div>
  </section>
</template>

<script setup>
  import { computed } from 'vue';
  import { useI18n } from 'vue-i18n';

  import FeaturedProjectCard from '@/components/cards/FeaturedProjectCard.vue';
  import ProjectCard from '@/components/cards/ProjectCard.vue';
  
  const { t: $t } = useI18n();
  const featuredProjects = computed(() => [
    {
      link: 'https://github.com/red-aero',
      repository: 'https://github.com/red-aero',
      name: 'Github projects',
      description: $t('PROJECTS.JSON_SEARCHER'),
      stack: ['C++, HTML, CSS, TS, JS, VUE'],
      image: 'https://media.giphy.com/media/26tn33aiTi1jkl6H6/giphy.gif?cid=ecf05e47t432mk2xoi8gqr30tu0hfpp3ehxpc0o2jpl5t5gm&ep=v1_gifs_search&rid=giphy.gif&ct=g'
    },
    
  ]);

  const projects = [];
</script>

<style lang="scss" scoped>
  #projects {
    display: flex;
    justify-content: center;
    flex-direction: column;
    background: var(--details-background);

    h2 {
      display: flex;
      align-items: center;
      font-size: 1.5rem;
      font-weight: 700;
      margin-bottom: 2.5rem;
      color: var(--secondary-text);

      &::before {
      content: '';
      display: block;
      position: relative;
      width: 50%;
      height: 1px;
      margin-right: 20px;
      background-color: var(--default-border);
    }

      &::after {
        content: '';
        display: block;
        position: relative;
        width: 50%;
        height: 1px;
        margin-left: 20px;
        background-color: var(--default-border);
      }
    }

    .featured-project-cards {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: start;
      flex-wrap: wrap;
      gap: 3rem;
      margin-top: 2rem;
    }

    .project-cards {
      margin-top: 3rem;
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 1rem;
    }

    .coming-soon-message {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100%;
      font-weight: 700;
      color: var(--secondary-text);
    }
  }
</style>