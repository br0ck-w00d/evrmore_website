<script lang="ts">
import { defineComponent, ref, computed } from 'vue'
import cateImage from '@/assets/projects/cate.png'
import magicImage from '@/assets/wallets/magic.svg'
import evrlandImage from '@/assets/faucets/evrland.svg'

export default defineComponent({
  name: 'ProjectsSectionTwo',
  props: {
    reverse: {
      type: Boolean,
      default: false
    },
    backgroundImageName: {
      type: String,
      required: true
    }
  },
  setup() {
    const gridItems = ref([
      { text: 'EvrLand', image: evrlandImage },
      { text: 'CateCoins', image: cateImage },
      { text: 'Magic', image: magicImage }
    ])

    const topRowItems = computed(() =>
      gridItems.value.length === 3 ? [gridItems.value[0]] : gridItems.value.slice(0, 2)
    )

    const bottomRowItems = computed(() =>
      gridItems.value.length === 3 ? gridItems.value.slice(1) : gridItems.value.slice(2)
    )

    const handleClick = (itemText: string) => {
      console.log('Clicked', itemText)
      let url = ''
      switch (itemText) {
        case 'EvrLand':
          url = 'https://www.evrland.net/'
          break
        case 'CateCoins':
          url = 'https://www.catecoins.com'
          break
        case 'Magic':
          url = 'https://www.x.com/magicwalletapp'
          break
        default:
          console.log('No URL defined for', itemText)
          return
      }

      if (url) {
        window.open(url, '_blank', 'noopener,noreferrer')
      }
    }

    return { gridItems, topRowItems, bottomRowItems, handleClick }
  }
})
</script>

<template>
  <section class="projectOne-section">
    <v-container class="d-flex justify-center">
      <v-row class="card-row">
        <v-col cols="12" xs="12" sm="12" md="4" lg="4" xl="4" class="col-title">
          <h2 class="section-title">Showcase</h2>
        </v-col>
        <v-col cols="12" xs="12" sm="12" md="4" lg="4" xl="4" class="col-image">
          <div class="col-wrapper">
            <div
              v-for="(item, index) in topRowItems"
              :key="index"
              @click="handleClick(item.text)"
              class="card-content"
            >
              <img :src="item.image" :alt="item.text" class="project-image" />
              <p class="placeholder-text">{{ item.text }}</p>
            </div>
          </div>
          <div class="col-wrapper">
            <div
              v-for="(item, index) in bottomRowItems"
              :key="index + topRowItems.length"
              @click="handleClick(item.text)"
              class="card-content"
            >
              <img :src="item.image" :alt="item.text" class="project-image" />
              <p class="placeholder-text">{{ item.text }}</p>
            </div>
          </div>
        </v-col>
      </v-row>
    </v-container>
  </section>
</template>

<style scoped lang="scss">
.projectOne-section {
  height: 650px;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  background-image: url('@/assets/landing_sections/landing_section_f8.png');
  background-size: cover;
  background-position: center;

  .card-row {
    max-width: 1200px;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
  }

  .col-title {
    display: flex;
    flex-direction: column;
    justify-content: start;
  }

  .col-image {
    display: flex;
    flex-direction: column;
    justify-content: start;
  }

  .section-title {
    font-family: Futura, sans-serif;
    font-size: 2.5rem;
    font-weight: 700;
    text-align: start;
  }

  .col-wrapper {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 4rem;
  }

  .card-content {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin-bottom: 2rem;
    cursor: pointer;
    transition: transform 0.2s ease;

    &:active {
      transform: scale(0.98);
    }
  }

  .project-image {
    width: 160px;
    height: 160px;
    margin-bottom: 1rem;
    cursor: pointer;
    transition: transform 0.2s ease;

    &:hover {
      transform: scale(1.05);
    }

    &:active {
      transform: scale(0.98);
    }
  }
}

@media (max-width: 959px) {
  .projectOne-section {
    height: auto;
    min-height: 650px;

    .card-row {
      flex-direction: column;
      flex-wrap: nowrap;
      margin-top: -350px;
    }

    .col-title {
      justify-content: end;
      height: 100px;
    }

    .col-image {
      justify-content: center;
    }

    .section-title {
      text-align: center;
    }

    .project-image {
      width: 120px;
      height: 120px;
    }
  }
}

@media (max-width: 599px) {
  .projectOne-section {
    height: 800px;

    .col-wrapper {
      flex-direction: column;
      gap: 0;
    }

    .project-image {
      width: 80px;
      height: 80px;
    }
  }
}
</style>
