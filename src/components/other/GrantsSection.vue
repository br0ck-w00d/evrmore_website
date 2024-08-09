<script lang="ts">
import { defineComponent, ref, computed } from 'vue'
import grantsImage from '@/assets/grants.svg'

export default defineComponent({
  name: 'GrantsSection',
  setup() {
    const resourceItems = ref([
      {
        text: 'Coming Soon',
        image: grantsImage,
        url: 'https://evrmore.com/initiatives'
      },
      {
        text: 'Coming Soon',
        image: grantsImage,
        url: 'https://evrmore.com/initiatives'
      },
      {
        text: 'Coming Soon',
        image: grantsImage,
        url: 'https://evrmore.com/initiatives'
      },
      {
        text: 'Coming Soon',
        image: grantsImage,
        url: 'https://evrmore.com/initiatives'
      },
      {
        text: 'Coming Soon',
        image: grantsImage,
        url: 'https://evrmore.com/initiatives'
      },
      {
        text: 'Coming Soon',
        image: grantsImage,
        url: 'https://evrmore.com/initiatives'
      }
    ])

    const currentPage = ref(0)
    const itemsPerPage = 3

    const totalPages = computed(() => Math.ceil(resourceItems.value.length / itemsPerPage))

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
  <section class="grants-section">
    <v-container>
      <div class="text-center section-title">
        <h2>Grants</h2>
        <p>The Evrmore Foundation</p>
      </div>
      <div class="resource-carousel">
        <v-btn icon @click="prevPage" class="carousel-btn" color="#C2C2C2">
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
        <v-btn icon @click="nextPage" class="carousel-btn" color="#C2C2C2">
          <v-icon color="white" size="32">mdi-chevron-right</v-icon>
        </v-btn>
      </div>
    </v-container>
  </section>
</template>

<style scoped lang="scss">
.grants-section {
  height: 450px;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;

  .section-title {
    margin-bottom: 2rem;

    h2 {
      font-family: 'Futura', sans-serif;
      font-size: 3rem;
      font-weight: bold;
      margin-bottom: 0.25rem;
    }

    p {
      font-family: 'Roboto', sans-serif;
      font-size: 1.25rem;
      font-weight: 400;
      line-height: 1.6;
      opacity: 0.67;
    }
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
  .grants-section {
    height: auto;
    min-height: 450px;
    padding: 2rem 0;

    .section-title {
      h2 {
        font-size: 2rem;
      }
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
  .grants-section {
    .section-title {
      h2 {
        font-size: 1.75rem;
      }
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
