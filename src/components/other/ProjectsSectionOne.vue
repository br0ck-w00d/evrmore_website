<script lang="ts">
import { defineComponent, ref, computed } from 'vue'
import satoriImage from '@/assets/projects/satori.png'
import littleWarriorsImage from '@/assets/projects/little_warriors.png'
import darkMemeImage from '@/assets/projects/dark_meme.png'

export default defineComponent({
  name: 'ProjectsSectionOne',
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
  setup(props) {
    const gridItems = ref([
      { text: 'Satori (AI)', image: satoriImage },
      { text: 'Little Warriors', image: littleWarriorsImage },
      { text: 'Dark Meme', image: darkMemeImage }
    ])

    const topRowItems = computed(() =>
      gridItems.value.length === 3 ? [gridItems.value[0]] : gridItems.value.slice(0, 2)
    )

    const bottomRowItems = computed(() =>
      gridItems.value.length === 3 ? gridItems.value.slice(1) : gridItems.value.slice(2)
    )

    const backgroundImageComputed = computed(() => {
      return new URL(`/src/assets/landing_sections/${props.backgroundImageName}`, import.meta.url)
        .href
    })

    const handleClick = (itemText: string) => {
      console.log('Clicked', itemText)
      switch (itemText) {
        case 'Satori (AI)':
          window.open('https://www.satorinet.io', '_blank')
          break
        case 'Little Warriors':
          window.open('https://x.com/litl_warriors', '_blank')
          break
        case 'Dark Meme':
          window.open('https://www.darkmemecoin.com/', '_blank')
          break
        default:
          break
      }
    }

    return { gridItems, topRowItems, bottomRowItems, handleClick, backgroundImageComputed }
  }
})
</script>

<template>
  <section class="projectOne-section">
    <v-container class="d-flex justify-center">
      <v-row class="card-row">
        <v-col cols="12" xs="12" sm="12" md="4" lg="4" xl="4" order-md="2" class="col-title">
          <h2 class="section-title">Spotlight</h2>
        </v-col>
        <v-col cols="12" xs="12" sm="12" md="4" lg="4" xl="4" order-md="1" class="col-image">
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
  height: 450px;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;

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
    text-align: right;
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
  }

  .project-image {
    width: 160px;
    height: 160px;
    margin-bottom: 1rem;
    cursor: pointer;
    transition:
      transform 0.2s ease,
      opacity 0.3s ease;

    &:hover {
      transform: scale(1.05);
      z-index: 1;
    }

    &:active {
      transform: scale(0.95);
    }
  }
}

@media (max-width: 959px) {
  .projectOne-section {
    height: auto;
    min-height: 450px;

    .card-row {
      flex-direction: column;
      flex-wrap: nowrap;
      margin-top: -350px;
    }

    .col-title {
      justify-content: end;
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
    height: 600px;

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
