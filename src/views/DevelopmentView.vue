<script lang="ts">
import { defineComponent } from 'vue'
import LandingSectionSeven from '@/components/landing/LandingSectionSeven.vue'
import LandingSectionEight from '@/components/landing/LandingSectionEight.vue'
import { useToolbarStore } from '../store/toolbar-store.pinia'
import LandingSectionSix from '@/components/landing/LandingSectionSix.vue'
import GrantsSection from '@/components/other/GrantsSection.vue'
import CodeSection from '@/components/other/CodeSection.vue'
import DevChatSection from '@/components/other/DevChatSection.vue'

export default defineComponent({
  name: 'DevelopmentView',
  components: {
    GrantsSection,
    CodeSection,
    LandingSectionSix,
    DevChatSection,
    LandingSectionSeven,
    LandingSectionEight
  },
  setup() {
    const toolbarStore = useToolbarStore()
    toolbarStore.setToolbarColor('black')
    return {}
  }
})
</script>

<template>
  <div class="landing-container">
    <!-- Header Section -->
    <section class="header-section">
      <div class="overlay-content">
        <v-container class="content-container d-flex flex-column justify-center align-center h-100">
          <div class="header-content">
            <h1 class="header-title">Development</h1>
            <p class="header-subtitle">Building the Future</p>
          </div>
          <div class="image-wrapper">
            <img
              src="@/assets/roadmap/development.svg"
              alt="Marketing Illustration"
              class="marketing-image"
            />
          </div>
        </v-container>
      </div>
    </section>

    <!-- Sections -->
    <div class="landing-sections-container">
      <GrantsSection />
      <CodeSection />
      <LandingSectionSix section-title="Roadmap" background-image-name="landing_section_ff.svg" />
      <DevChatSection />
      <LandingSectionSeven background-image-name="landing_section_2f8.png" />
      <LandingSectionEight />
    </div>
  </div>
</template>

<style scoped lang="scss">
.header-section {
  background-image: url('@/assets/landing_sections/view_header.png');
  background-size: cover;
  background-position: center;
  height: 850px;
  overflow: hidden;

  .overlay-content {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .content-container {
    text-align: center;
  }

  .header-content {
    color: rgba(0, 0, 0, 0.87);
    margin-bottom: 2rem;
  }

  .header-title {
    font-family: 'Futura', sans-serif;
    font-size: 4rem;
    font-weight: bold;
    line-height: 1.2;
    margin-bottom: 0.5rem;
  }

  .header-subtitle {
    font-family: 'Roboto', sans-serif;
    font-weight: 500;
    font-size: 1.5rem;
  }

  .image-wrapper {
    width: 100%;
    max-width: 600px;
    margin: 0 auto;
  }

  .marketing-image {
    max-width: 100%;
    height: auto;
  }
}

@media (max-width: 959px) {
  .header-section {
    .header-title {
      font-size: 3rem;
    }
    .header-subtitle {
      font-size: 1.25rem;
    }
  }
}

@media (max-width: 599px) {
  .header-section {
    height: 100vh;

    .header-title {
      font-size: 2.5rem;
    }
    .header-subtitle {
      font-size: 1rem;
    }
    .image-wrapper {
      max-width: 90%;
    }
  }
}
</style>
