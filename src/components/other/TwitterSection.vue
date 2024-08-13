<script lang="ts">
import { defineComponent, ref, computed } from 'vue'
import twitterImage from '@/assets/socials/twitter.svg'
import evrmoreImage from '@/assets/logo_pack/logo_pack.svg'
import evrmoreOldImage from '@/assets/logo_pack/logo_old.png'
import evrFoundationImage from '@/assets/socials/evr_foundation.svg'
import evrDefiImage from '@/assets/socials/evr_defi.jpeg'
import namelessEvrImage from '@/assets/socials/nameless_evr.jpeg'
import { useDisplay } from 'vuetify'

export default defineComponent({
  name: 'TwitterSection',
  setup() {
    const resourceItems = ref([
      {
        text: 'Evrmore Official',
        image: evrmoreImage,
        url: 'https://x.com/evrmoreofficial'
      },
      {
        text: 'Evrmore Foundation',
        image: evrFoundationImage,
        url: 'https://x.com/evrfoundation'
      },
      {
        text: 'Evrmore DeFi',
        image: evrDefiImage,
        url: 'https://x.com/evrdefi'
      },
      {
        text: 'Evr 中文社区',
        image: evrmoreOldImage,
        url: 'https://x.com/LBJRL1BHIQ90243'
      },
      {
        text: 'Nameless 4 Evrmore',
        image: namelessEvrImage,
        url: 'https://x.com/NamelessEvrmore'
      },
      {
        text: 'Coming Soon',
        image: twitterImage,
        url: 'https://evrmore.com/initiatives'
      }
    ])

    const { smAndDown } = useDisplay()

    const currentPage = ref(0)
    const itemsPerPage = computed(() => (smAndDown.value ? 1 : 3))

    const totalPages = computed(() => Math.ceil(resourceItems.value.length / itemsPerPage.value))

    const handleClick = (url: string) => {
      window.open(url, '_blank')
    }

    const nextPage = () => {
      currentPage.value = (currentPage.value + 1) % totalPages.value
    }

    const prevPage = () => {
      currentPage.value = (currentPage.value - 1 + totalPages.value) % totalPages.value
    }

    return { resourceItems, handleClick, currentPage, nextPage, prevPage, itemsPerPage }
  }
})
</script>

<template>
  <section class="twitter-section">
    <v-container>
      <h2 class="section-title">Twitter</h2>
      <div class="resource-carousel">
        <v-btn icon @click="prevPage" class="carousel-btn" color="#c2c2c2">
          <v-icon color="white" size="32">mdi-chevron-left</v-icon>
        </v-btn>
        <div class="resource-window">
          <v-window v-model="currentPage" class="resource-window-inner">
            <v-window-item v-for="n in Math.ceil(resourceItems.length / itemsPerPage)" :key="n">
              <div class="resource-grid">
                <div
                  v-for="(item, index) in resourceItems.slice(
                    (n - 1) * itemsPerPage,
                    n * itemsPerPage
                  )"
                  :key="index"
                  class="resource-item"
                  @click="handleClick(item.url)"
                >
                  <div class="image-container">
                    <img :src="item.image" :alt="item.text" class="resource-image" />
                  </div>
                  <p class="resource-text">{{ item.text }}</p>
                </div>
              </div>
            </v-window-item>
          </v-window>
        </div>
        <v-btn icon @click="nextPage" class="carousel-btn" color="#c2c2c2">
          <v-icon color="white" size="32">mdi-chevron-right</v-icon>
        </v-btn>
      </div>
    </v-container>
  </section>
</template>

<style scoped lang="scss">
.twitter-section {
  height: 650px;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  background-image: url('@/assets/landing_sections/landing_section_f8.png');
  background-size: cover;
  background-position: center;

  .section-title {
    font-family: 'Futura', sans-serif;
    font-size: 3rem;
    font-weight: bold;
    color: #000000;
    text-align: center;
    margin-bottom: 0.25rem;
  }

  .resource-carousel {
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

  .resource-window {
    width: 100%;
    overflow: hidden;
    padding: 2rem 0;
  }

  .resource-window-inner {
    overflow: visible;
  }

  .resource-grid {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 4rem;
  }

  .resource-item {
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

  .image-container {
    width: 160px;
    height: 160px;
    border-radius: 80px;
    margin-bottom: 10px;
    overflow: hidden;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .resource-image {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  .resource-text {
    font-family: 'Roboto', sans-serif;
    font-size: 1rem;
    font-weight: 500;
    line-height: 1.6;
    opacity: 0.67;
    text-align: center;
  }
}

@media (max-width: 959px) {
  .twitter-section {
    height: auto;
    min-height: 650px;
    padding: 4rem 0;

    .section-title {
      font-size: 2rem;
    }

    .resource-carousel {
      max-width: 400px;
    }

    .resource-grid {
      flex-direction: column;
      gap: 1.5rem;
    }

    .image-container {
      width: 120px;
      height: 120px;
    }
  }
}

@media (max-width: 599px) {
  .twitter-section {
    .section-title {
      font-size: 1.75rem;
    }

    .resources-grid {
      gap: 1rem;
    }

    .image-container {
      width: 100px;
      height: 100px;
      border-radius: 50px;
    }

    .resource-text {
      font-size: 0.9rem;
    }
  }
}
</style>
