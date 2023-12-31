<template>
  <section id="career">
    <div class="container appear-on-scroll">
      <h2>{{ $t('CAREER.TITLE') }}</h2>

      <div class="places-container">
        <div class="buttons-container">
          <div 
            class="current-selected-marker"
            :style="selectedMarkerStyle"
          />
          <button
            v-for="(place, index) in placesTimeline"
            :key="index"
            :class="{ active: currentPlaceIndex === index }"
            @click="setPlaceAsActive(index)"
          >
            {{ place.name }}
          </button>
        </div>

        <Transition 
          name="fade"
          mode="out-in"
        >
          <div 
            class="active-place-content"
            :key="currentPlaceIndex"
          >
            <div class="title">
              <span>{{ currentPlace.role }} at </span>
              <a 
                class="place-name"
                :href="currentPlace.link"
                target="_blank"
              >
                {{ currentPlace.name }}
              </a>
            </div>

            <div class="period">
              {{ currentPlace.period }}
            </div>

            <ul class="description">
              <li 
                v-for="i in currentPlace.paragraphsQtt"
                :key="i"
              >
                {{ $t(`CAREER.${currentPlace.key}.RESUME_${i}`) }}
              </li>
            </ul>
          </div>
        </Transition>
      </div>
    </div>
  </section>
</template>

<script setup>
  import { ref, computed } from 'vue';
  import { useI18n } from 'vue-i18n';

  const { t: $t } = useI18n();

  const currentPlaceIndex = ref(0);
  const currentPlace = computed(() => (placesTimeline[currentPlaceIndex.value] || {}));

  const selectedMarkerStyle = computed(() => {
    // If is mobile
    if (window.innerWidth <= 768) {
      return {
        left: `${currentPlaceIndex.value * 25}%`,
      };
    }

    return {
      top: `${currentPlaceIndex.value * 25}%`,
    };
  });

  const placesTimeline = [
    { 
      name: 'HIGH SCHOOL',
      key: 'HIGH SCHOOL',
      paragraphsQtt: 3,
      role: 'Student',
      period: 'from 2020 to 2022',
      
   },
    { 
      name: 'DEAKIN UNIVERSITY',
      key: 'DEAKIN UNIVERSITY',
      paragraphsQtt: 2,
      role: 'Student',
      period: 'from 2023 until now',
      link: 'https://www.deakin.edu.au',
    },
    { 
      name: 'CURRENT',
      key: 'CURRENT',
      paragraphsQtt: 1,
      role: 'Trainee',
      period: 'Always',
      
    },
    
  ]

  const setPlaceAsActive = (index) => {
    currentPlaceIndex.value = index;
  }
</script>

<style lang="scss" scoped>
  #career {
    min-height: 90vh;
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
        width: 100%;
        height: 1px;
        margin-left: 20px;
        background-color: var(--default-border);
      }
    }

    .places-container {
      display: flex;
      justify-content: center;
      align-items: start;
      flex-wrap: wrap;
      gap: 0.5rem;
      margin-top: 2rem;
      

      & .buttons-container {
        display: flex;
        flex-direction: column;
        
        button {
          margin: 0;
          margin-left: 1px;
          padding: 1rem;
          border: 0;
          border-left: 1px solid var(--default-border);
          background: transparent;
          cursor: pointer;
          transition: all 0.2s ease-in-out;
          color: var(--disabled-text);
          font-size: 1rem;
          font-weight: 600;
          border-radius: 0 .5rem .5rem 0;

          &:hover {
            background-color: var(--default-border);
          }

          &.active {
            background-color: var(--default-border) !important;
            color: var(--details-background);
          }
        }

        .current-selected-marker {
          width: 3px;
          height: 25%;
          background-color: var(--details-background);
          position: absolute;
          left: 0;
          top: 0;
          transition: all 0.3s ease-in-out;
          z-index: 10;
        }
      }

      & .active-place-content {
        flex: 1;
        display: flex;
        flex-direction: column;
        padding: 0 2rem;
        height: 350px;

        & .title {
          font-size: 1.5rem;
          font-weight: 600;
          
          & .place-name {
            color: var(--secondary-text);
            font-weight: 600;
            text-decoration: none;
            transition: all 0.2s ease-in-out;

            &::after {
              content: '';
              position: absolute;
              width: 100%;
              transform: scaleX(0);
              height: 3px;
              bottom: 0px;
              left: 0;
              background: var(--secondary-text);
              transform-origin: bottom right;
              transition: transform 0.25s ease-out;
            }

            &:hover::after {
              transform: scaleX(1);
              transform-origin: bottom left;
            }
          }
        }

        & .period {
          font-size: 1rem;
          color: var(--secondary-text);
          margin-bottom: 1rem;
        }

        & .description {
          font-size: 1rem;
          color: var(--secondary-text);
          line-height: 1.5rem;
          text-align: justify;
          max-width: 800px;
          display: flex;
          flex-direction: column;
          gap: 0.5rem;
          list-style-type: circle;
        }
      }
    }
  }

  @media (max-width: 768px) {
    #career {
      .places-container {
        display: flex;
        flex-direction: column;

        & .buttons-container {
          flex-direction: row;
          width: 100%;

          button {
            width: 25%;
            border: none;
            border-top: 1px solid var(--default-border);
            padding: 0.5rem 0.25rem;
            border-radius: 0 0 .5rem .5rem;
          }
        }

        & .current-selected-marker {
          height: 3px !important;
          width: 25% !important;
        }

        & .active-place-content {
          padding: 0 !important;

          .title, .period {
            text-align: center;
          }	
        }

        ul {
          padding: .5rem;
        }
      }
    }
  }
</style>