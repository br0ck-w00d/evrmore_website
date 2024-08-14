<script lang="ts">
import { defineComponent, computed, ref, onMounted } from 'vue'
import { useDisplay } from 'vuetify'
import LandingSectionSix from '@/components/landing/LandingSectionSix.vue'
import LandingSectionSeven from '@/components/landing/LandingSectionSeven.vue'
import LandingSectionEight from '@/components/landing/LandingSectionEight.vue'
import { useToolbarStore } from '../store/toolbar-store.pinia'
import LandingSectionChooseEvr from '@/components/landing/LandingSectionChooseEvr.vue'
import LandingSectionTeam from '@/components/landing/LandingSectionTeam.vue'
import LandingSectionLearnMore from '@/components/landing/LandingSectionLearnMore.vue'

// Import SVG images for cards
import defiRebelsImage from '@/assets/socials/community.svg'
import hackerImage from '@/assets/choose_evr/hacker.svg'
import saferSimplerImage from '@/assets/choose_evr/versatile.svg'

export default defineComponent({
  name: 'LandingView',
  components: {
    LandingSectionChooseEvr,
    LandingSectionTeam,
    LandingSectionSix,
    LandingSectionLearnMore,
    LandingSectionSeven,
    LandingSectionEight
  },
  setup() {
    const { xs } = useDisplay()
    const iconSize = computed(() => (xs.value ? '1.5rem' : '2.5rem'))

    const toolbarStore = useToolbarStore()
    toolbarStore.setToolbarColor('white')

    const cardAnimations = ref(['', '', ''])

    onMounted(() => {
      setTimeout(() => {
        cardAnimations.value[0] = 'animate'
        setTimeout(() => {
          cardAnimations.value[1] = 'animate'
          setTimeout(() => {
            cardAnimations.value[2] = 'animate'
          }, 500)
        }, 500)
      }, 500)
    })

    return {
      iconSize,
      cardAnimations,
      cards: [
        {
          title: 'DeFi Rebels',
          image: defiRebelsImage
        },
        {
          title: 'Taking on EVMs',
          image: hackerImage
        },
        {
          title: 'Safe & Simple',
          image: saferSimplerImage
        }
      ]
    }
  }
})
</script>

<template>
  <div class="landing-container">
    <!-- Header Section -->
    <section class="header-section">
      <v-container fluid class="header-wrapper">
        <div class="header-content-wrapper">
          <h1 class="header-title">Evrmore</h1>
          <img src="@/assets/evrmore_logo.svg" alt="Evrmore Logo" class="header-logo" />
        </div>
        <v-container fluid class="container-center card-container">
          <v-row justify="center" align="center" class="card-row">
            <v-col
              cols="12"
              xs="12"
              sm="8"
              md="4"
              lg="4"
              xl="3"
              v-for="(card, index) in cards"
              :key="index"
              class="card-col"
            >
              <v-sheet
                :class="['card d-flex align-center justify-space-between', cardAnimations[index]]"
              >
                <img :src="card.image" :alt="card.title" class="card-image" />
                <h3 class="card-title">{{ card.title }}</h3>
              </v-sheet>
            </v-col>
          </v-row>
        </v-container>
      </v-container>
    </section>

    <!-- Sections -->
    <div class="landing-sections-container">
      <LandingSectionChooseEvr background-image-name="landing_section_1.png" />
      <LandingSectionTeam background-image-name="landing_section_f8.png" />
      <LandingSectionSix
        section-title="Development"
        background-image-name="landing_section_ff.svg"
      />
      <LandingSectionLearnMore background-image-name="landing_section_94.png" />
      <LandingSectionSeven background-image-name="landing_section_294.png" />
      <LandingSectionEight />
    </div>
  </div>
</template>

<style scoped lang="scss">
.header-section {
  background-image: url('@/assets/landing_sections/header_background.png');
  background-size: cover;
  background-position: center;
  padding: 1rem;
  height: 100vh;
  min-height: 850px;

  .header-wrapper {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    height: 95%;
  }

  .header-content-wrapper {
    padding-top: 10vh;
    text-align: center;
    color: white;
  }

  .header-title {
    font-family: 'Futura', sans-serif;
    font-size: 6rem;
    font-weight: bold;
    line-height: 4.8rem;
    margin-bottom: 2rem;
  }

  .header-logo {
    width: 160px;
    height: 160px;
  }

  .card-row {
    width: 100%;
  }

  .card-col {
    display: flex;
    justify-content: center;
    padding: 1rem;
  }

  .card {
    background-color: rgba(255, 255, 255, 0.8);
    padding: 1rem;
    border-radius: 45px;
    text-align: center;
    flex-direction: column;
    width: 100%;
    height: 100%;
    transition: all 0.3s ease;

    &:hover {
      transform: scale(1.02);
    }

    &.animate {
      animation: growShrink 1s ease;
    }
  }

  .card-image {
    height: 300px;
    width: 300px;
    object-fit: contain;
    margin-bottom: 1rem;
  }

  .card-title {
    font-family: 'Roboto', sans-serif;
    font-size: 2rem;
    font-weight: bold;
    color: #000000;
    opacity: 0.72;
  }

  .container-center {
    display: flex;
    justify-content: center;
  }

  .card-container {
    max-width: 2400px;
    width: 100%;
  }
}

@keyframes growShrink {
  0%,
  100% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.05);
  }
}

.finance-section,
.assets-section,
.swaps-section,
.built-section,
.wallet-section,
.development-section {
  padding: 4rem 0;
  background-color: #ffffff;

  h2 {
    font-family: 'Futura', sans-serif;
    font-size: 2.5rem;
    font-weight: bold;
    margin-bottom: 1rem;
  }

  p {
    font-family: 'Roboto', sans-serif;
    font-size: 1.1rem;
    line-height: 1.6;
  }

  .section-image {
    max-width: 100%;
    height: auto;
  }
}

.assets-section,
.built-section,
.development-section {
  background-color: #000000;
  color: #ffffff;
}

.swaps-section,
.wallet-section {
  background-color: #031a32;
  color: #ffffff;
}

@media (max-width: 1279px) {
  .header-section {
    height: auto;

    .card {
      height: 410px;
      padding: 1.75rem;
    }

    .card-image {
      width: 250px;
      height: 250px;
    }

    .card-title {
      font-size: 2.25rem; // Slightly reduced for better fit
    }
  }
}

@media (max-width: 959px) {
  .header-section {
    .card {
      padding: 1.5rem;
    }
    .card-title {
      font-size: 2rem; // Further reduced for medium screens
    }
  }
}

@media (max-width: 599px) {
  .header-section {
    padding: 0;

    .header-title {
      font-size: 4rem;
      line-height: 3.2rem;
    }

    .header-logo {
      width: 100px;
      height: 100px;
    }

    .card {
      height: auto;
      padding: 2rem;
    }

    .card-col {
      padding: 1rem 0;
    }

    .card-image {
      width: 200px;
      height: 200px;
    }

    .card-title {
      font-size: 1.75rem; // Adjusted for mobile screens
    }
  }
}
</style>
