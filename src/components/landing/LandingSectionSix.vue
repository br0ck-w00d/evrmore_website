<script lang="ts">
import { computed, defineComponent, ref } from 'vue'
import evrlightImage from '@/assets/roadmap/evrlight.svg'
import developmentImage from '@/assets/roadmap/asset_tolls.svg'
import launchImage from '@/assets/roadmap/launch.svg'
import websiteImage from '@/assets/roadmap/website.svg'
import whitePaperImage from '@/assets/roadmap/white_paper.svg'
import bearMarketImage from '@/assets/roadmap/bear_market.svg'

export default defineComponent({
  name: 'LandingSectionSix',
  props: {
    reverse: {
      type: Boolean,
      default: false
    },
    backgroundImageName: {
      type: String,
      required: true
    },
    sectionTitle: {
      type: String,
      required: true
    }
  },
  setup(props) {
    const roadmapItems = ref([
      {
        image: whitePaperImage,
        text: 'White Paper',
        subtext: '09/2022',
        completed: true,
        active: true,
        link: 'https://github.com/evrmoreorg/whitepaper/blob/master/Evrmore_Whitepaper_2022-09-12.pdf'
      },
      {
        image: launchImage,
        text: 'Launch',
        subtext: '11/2022',
        completed: true,
        active: true,
        link: 'https://bitcointalk.org/index.php?topic=5416790.0'
      },
      {
        image: bearMarketImage,
        text: 'Bear Market',
        subtext: '2023',
        completed: true,
        active: true,
        link: '#'
      },
      {
        image: websiteImage,
        text: 'Website',
        subtext: '04/2024',
        completed: true,
        active: true,
        link: 'https://evrmore.com'
      },
      {
        image: evrlightImage,
        text: 'EvrLight',
        subtext: 'In Development',
        completed: false,
        active: true,
        link: 'https://hans-schmidt.github.io/mastering_evrmore/evrlight_and_nostr4evr/evrlight_and_nostr4evr.html'
      },
      {
        image: developmentImage,
        text: 'Asset Tolls',
        subtext: 'In Development',
        completed: false,
        active: true,
        link: '#'
      },
      {
        image: developmentImage,
        text: 'Expiring NFTs',
        subtext: 'Planned Early 2025',
        completed: false,
        active: false,
        link: '#'
      },
      {
        image: developmentImage,
        text: 'Consumables',
        subtext: 'Planned Early 2025',
        completed: false,
        active: false,
        link: '#'
      },
      {
        image: developmentImage,
        text: 'Covenants',
        subtext: 'Planned 2025',
        completed: false,
        active: false,
        link: ''
      },
      {
        image: developmentImage,
        text: 'Vaults',
        subtext: 'Planned 2025',
        completed: false,
        active: false,
        link: '#'
      },
      {
        image: developmentImage,
        text: 'AMM Vaults',
        subtext: 'TBD',
        completed: false,
        active: false,
        link: '#'
      }
    ])

    const backgroundImageComputed = computed(() => {
      return new URL(`/src/assets/landing_sections/${props.backgroundImageName}`, import.meta.url)
        .href
    })

    const handleClick = (link: string) => {
      if (link) {
        window.open(link, '_blank')
      }
    }

    const currentPage = ref(1)
    const itemsPerPage = 3

    const totalPages = computed(() => Math.ceil(roadmapItems.value.length / itemsPerPage))

    const nextPage = () => {
      currentPage.value = (currentPage.value + 1) % totalPages.value
    }

    const prevPage = () => {
      currentPage.value = (currentPage.value - 1 + totalPages.value) % totalPages.value
    }

    return {
      roadmapItems,
      handleClick,
      backgroundImageComputed,
      currentPage,
      nextPage,
      prevPage,
      itemsPerPage
    }
  }
})
</script>

<template>
  <!-- <section class="landing-section landing-section-six" :class="{ reverse: reverse }">
    <img :src="backgroundImageComputed" alt="Section Background" class="section-background" />
    <div class="content-wrapper">
      <v-container class="d-flex flex-column align-center justify-center h-100">
        <div class="text-content text-center">
          <h2>{{ sectionTitle }}</h2>
        </div>
        <div class="roadmap-carousel">
          <v-btn icon @click="prevPage" class="carousel-nav left" color="#4d93c7">
            <v-icon color="white" size="36">mdi-chevron-left</v-icon>
          </v-btn>
          <div class="roadmap-window">
            <v-window v-model="currentPage" class="roadmap-window-inner">
              <v-window-item v-for="n in Math.ceil(roadmapItems.length / itemsPerPage)" :key="n">
                <div class="roadmap-grid">
                  <div
                    v-for="(item, index) in roadmapItems.slice(
                      (n - 1) * itemsPerPage,
                      n * itemsPerPage
                    )"
                    :key="index"
                    class="roadmap-item"
                    @click="handleClick(item.link)"
                    :style="{ opacity: item.completed || item.active ? 1 : 0.37 }"
                  >
                    <div class="circle-container">
                      <img :src="item.image" :alt="item.text" class="roadmap-image" />
                    </div>
                    <div class="roadmap-content">
                      <div class="radio-title-row">
                        <v-icon
                          :icon="
                            item.completed
                              ? 'mdi-check-circle-outline'
                              : 'mdi-checkbox-blank-circle-outline'
                          "
                          :color="
                            item.completed || item.active
                              ? 'rgba(0, 0, 0, 0.87)'
                              : 'rgba(0, 0, 0, 0.37)'
                          "
                          size="small"
                          class="roadmap-radio"
                        ></v-icon>
                        <p class="roadmap-title">{{ item.text }}</p>
                      </div>
                      <p class="roadmap-subtitle">{{ item.subtext }}</p>
                    </div>
                  </div>
                </div>
              </v-window-item>
            </v-window>
          </div>
          <v-btn icon @click="nextPage" class="carousel-nav right" color="#4d93c7">
            <v-icon color="white" size="36">mdi-chevron-right</v-icon>
          </v-btn>
        </div>
      </v-container>
    </div>
  </section> -->
  <section class="develop-section">
    <v-container>
      <h2 class="section-title">Development</h2>
      <div class="roadmap-carousel">
        <v-btn icon @click="prevPage" class="carousel-btn" color="#4d93c7">
          <v-icon color="white" size="32">mdi-chevron-left</v-icon>
        </v-btn>
        <div class="roadmap-window">
          <v-window v-model="currentPage" class="roadmap-window-inner">
            <v-window-item v-for="n in Math.ceil(roadmapItems.length / itemsPerPage)" :key="n">
              <div class="roadmap-grid">
                <div
                  v-for="(item, index) in roadmapItems.slice(
                    (n - 1) * itemsPerPage,
                    n * itemsPerPage
                  )"
                  :key="index"
                  class="roadmap-item"
                  @click="handleClick(item.link)"
                  :style="{ opacity: item.completed || item.active ? 1 : 0.37 }"
                >
                  <div class="circle-container">
                    <img :src="item.image" :alt="item.text" class="roadmap-image" />
                  </div>
                  <div class="roadmap-content">
                    <div class="radio-title-row">
                      <v-icon
                        :icon="
                          item.completed
                            ? 'mdi-check-circle-outline'
                            : 'mdi-checkbox-blank-circle-outline'
                        "
                        :color="
                          item.completed || item.active
                            ? 'rgba(0, 0, 0, 0.87)'
                            : 'rgba(0, 0, 0, 0.37)'
                        "
                        size="small"
                        class="roadmap-radio"
                      ></v-icon>
                      <p class="roadmap-title">{{ item.text }}</p>
                    </div>
                    <p class="roadmap-subtitle">{{ item.subtext }}</p>
                  </div>
                </div>
              </div>
            </v-window-item>
          </v-window>
        </div>
        <v-btn icon @click="nextPage" class="carousel-btn" color="#4d93c7">
          <v-icon color="white" size="32">mdi-chevron-right</v-icon>
        </v-btn>
      </div>
    </v-container>
  </section>
</template>

<style scoped lang="scss">
.develop-section {
  height: 580px;
  width: 100%;
  display: flex;
  justify-self: center;
  align-items: center;
  padding: 2rem;

  .section-title {
    font-family: 'Futura', sans-serif;
    font-size: 3rem;
    font-weight: bold;
    color: #000000;
    text-align: center;
  }

  .roadmap-carousel {
    width: 100%;
    max-width: 960px;
    margin: 0 auto;
    display: flex;
    align-items: center;
    overflow: visible;
  }

  .carousel-btn {
    width: 48px;
    height: 48px;
  }

  .roadmap-window {
    width: 100%;
    overflow: hidden;
    padding: 2rem 0;
  }

  .roadmap-window-inner {
    overflow: visible;
  }

  .roadmap-grid {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 4rem;
  }

  .roadmap-item {
    display: flex;
    flex-direction: column;
    align-items: center;
    cursor: pointer;
    transition:
      transform 0.2s ease,
      opacity 0.3s ease;
    width: 100%;
    max-width: 200px;

    &:hover {
      transform: scale(1.05);
      z-index: 1;
    }

    &:active {
      transform: scale(0.95);
    }
  }

  .circle-container {
    width: 160px;
    height: 160px;
    border-radius: 50%;
    background-color: #e6eef2;
    display: flex;
    justify-content: center;
    align-items: center;
    overflow: hidden;
    margin-bottom: 1rem;
  }

  .roadmap-image {
    max-width: 70%;
    max-height: 70%;
    object-fit: contain;
  }

  .roadmap-content {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 100%;
  }

  .radio-title-row {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    margin-bottom: 0.1rem;
  }

  .roadmap-radio {
    margin-right: 8px;
  }

  .roadmap-title {
    font-family: 'Roboto', sans-serif;
    font-size: 1.25rem;
    font-weight: 500;
    text-align: center;
    margin: 0;
    color: #000000;
    opacity: 0.67;
  }

  .roadmap-subtitle {
    font-family: 'Roboto', sans-serif;
    font-size: 1rem;
    text-align: center;
    margin: 0;
    color: #000000;
    opacity: 0.67;
  }
}

@media (max-width: 1279px) {
  .develop-section {
    .carousel-btn {
      width: 36px;
      height: 36px;
    }

    .circle-container {
      width: 120px;
      height: 120px;
    }
  }
}

@media (max-width: 959px) {
  .develop-section {
    height: auto;

    .section-title {
      font-size: 2rem;
    }

    .roadmap-carousel {
      height: 750px;
      gap: 1.5rem;
    }

    .roadmap-grid {
      flex-direction: column;
      gap: 2rem;
    }

    .roadmap-title {
      font-size: 1.25rem;
    }

    .roadmap-subtitle {
      font-size: 0.9rem;
    }
  }
}

@media (max-width: 599px) {
  .develop-section {
    .section-title {
      font-size: 1.75rem;
    }

    .roadmap-carousel {
      height: 600px;
      gap: 1rem;
    }

    .circle-container {
      width: 100px;
      height: 100px;
    }

    .roadmap-title {
      font-size: 1rem;
    }

    .roadmap-subtitle {
      font-size: 0.8rem;
    }
  }
}
</style>
