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
import LandingSectionTop from '@/components/landing/LandingSectionTop.vue'
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
    LandingSectionEight,
    LandingSectionTop
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
    
  <LandingSectionTop />

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
</style>
