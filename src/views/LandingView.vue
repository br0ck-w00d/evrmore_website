<script lang="ts">
import { defineComponent, computed, ref, onMounted } from 'vue'
import { useDisplay } from 'vuetify'
import LandingSectionSix from '@/components/landing/LandingSectionSix.vue'
import LandingSectionSeven from '@/components/landing/LandingSectionSeven.vue'
import LandingSectionEight from '@/components/landing/LandingSectionEight.vue'
import { useToolbarStore } from '../store/toolbar-store.pinia'
import LandingSectionAdvantage from '@/components/landing/LandingSectionAdvantage.vue'
import LandingSectionTeam from '@/components/landing/LandingSectionTeam.vue'
import LandingSectionLearnMore from '@/components/landing/LandingSectionLearnMore.vue'

// Import SVG images for cards
import layerOneDefiImage from '@/assets/landing_sections/layer_one_defi.svg'
import hackerImage from '@/assets/advantage/hacker.svg'
import easySwapsImage from '@/assets/landing_sections/easy_swaps.svg'

export default defineComponent({
  name: 'LandingView',
  components: {
    LandingSectionAdvantage,
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
          title: 'Layer One DeFi',
          image: layerOneDefiImage
        },
        {
          title: 'No Contract Hacks',
          image: hackerImage
        },
        {
          title: 'Easy Swaps',
          image: easySwapsImage
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
      <img
        src="@/assets/landing_sections/header_background.svg"
        alt="Header Background"
        class="header-image"
      />
      <div class="overlay-content">
        <v-container class="content-container d-flex flex-column justify-space-between h-100">
          <div class="header-content-wrapper">
            <v-row justify="center" align="start" class="header-row">
              <v-col cols="12" class="text-center">
                <div class="header-content">
                  <h1 class="header-title">Evrmore</h1>
                  <img src="@/assets/evrmore_logo.svg" alt="Evrmore Logo" class="header-logo" />
                </div>
              </v-col>
            </v-row>
          </div>
          <div class="cards-wrapper">
            <v-container fluid>
              <v-row justify="center" align="center" class="card-row">
                <v-col
                  cols="12"
                  xs="12"
                  sm="6"
                  md="4"
                  lg="4"
                  xl="3"
                  v-for="(card, index) in cards"
                  :key="index"
                  class="card-col"
                >
                  <div :class="['card', cardAnimations[index]]">
                    <img :src="card.image" :alt="card.title" class="card-image" />
                    <h3 class="card-title">{{ card.title }}</h3>
                  </div>
                </v-col>
              </v-row>
            </v-container>
          </div>
        </v-container>
      </div>
    </section>

    <!-- Sections -->
    <div class="landing-sections-container">
      <LandingSectionAdvantage background-image-name="landing_section_1.svg" />
      <LandingSectionTeam background-image-name="landing_section_f8.svg" />
      <LandingSectionSix
        section-title="Development"
        background-image-name="landing_section_ff.svg"
      />
      <LandingSectionLearnMore background-image-name="landing_section_94.svg" />
      <LandingSectionSeven background-image-name="landing_section_294.svg" />
      <LandingSectionEight />
    </div>
  </div>
</template>

<style scoped lang="scss">
.header-section {
  position: relative;
  height: 100vh;
  overflow: hidden;

  .header-image {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  .overlay-content {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
  }

  .content-container {
    padding-top: 2rem;
    padding-bottom: 2rem;
  }

  .header-content-wrapper {
    padding-top: 10vh;
  }

  .header-content {
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

  .cards-wrapper {
    margin-bottom: 14vh;
    width: 100%;
  }

  .card-row {
    width: 100%;
    margin: 0;
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
    display: flex;
    flex-direction: column;
    justify-content: space-between;
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
    height: 250px;
    width: auto;
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
    .card {
      padding: 1.75rem;
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
    height: 150vh;

    .header-title {
      font-size: 4rem;
      line-height: 3.2rem;
    }
    .header-logo {
      width: 100px;
      height: 100px;
    }
    .card {
      padding: 1.25rem;
    }
    .card-title {
      font-size: 1.75rem; // Adjusted for mobile screens
    }
  }
}
</style>
