<template>
  <section id="contact">
    <div class="container appear-on-scroll">
      <h2>{{ $t('CONTACT.TITLE')}}</h2>

      <div class="contact-cards">
        <ContactCard
          v-for="(contact, index) in contacts"
          :key="index"
          :contact="contact"
        />
      </div>
    </div>
  </section>
</template>

<script setup>
  import ContactCard from '@/components/cards/ContactCard.vue';

  import { computed } from 'vue';
  import { useI18n } from 'vue-i18n';
  const { t: $t } = useI18n();

  const contacts = computed(() => [
    {
      icon: 'fa-solid fa-envelope',
      text: 's2230225115@deakin.edu.au',
      link: 's2230225115@deakin.edu.au'
    },
    {
      icon: 'fa-brands fa-github',
      text: 'Harshit(Git)',
      link: 'https://github.com/red-aero'
    },
    {
      icon: 'fa-brands fa-linkedin',
      text: 'Harshit(Linkedin)',
      link: 'https://www.linkedin.com/in/harshit-1296b8271'
    },
  ]);
</script>

<style lang="scss">
  #contact {
    min-height: 50vh;
    display: flex;
    justify-content: center;
    flex-direction: column;

    h2 {
      display: flex;
      align-items: center;
      font-size: 1.5rem;
      font-weight: 700;
      margin-bottom: 1rem;
      color: var(--secondary-text);

      &::before {
        content: '';
        display: block;
        position: relative;
        width: 50px;
        height: 1px;
        margin-right: 20px;
        background-color: var(--default-border);
      }
      &::after {
        content: '';
        display: block;
        position: relative;
        width: 530px;
        height: 1px;
        margin-left: 20px;
        background-color: var(--default-border);
      }
    }

    .contact-cards {
      display: flex;
      flex-direction: column;
      gap: 1rem;
    }
  }

  @media (max-width: 768px) {
    #contact {
      h2 {
        &::before, &::after {
          width: 50%;
        }
      }

      .contact-card {
        padding: 1rem;

        & .text {
          font-size: 1rem;
        }

        & .icon {
          margin-right: 0;
        }
      }
    }
  }
</style>