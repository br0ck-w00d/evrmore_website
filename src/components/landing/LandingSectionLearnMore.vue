<script lang="ts">
import { computed, defineComponent, ref } from 'vue'
import { useRouter } from 'vue-router'
import projectsImage from '@/assets/projects/projects.svg'
import miningImage from '@/assets/mining/mining_section_header_image.svg'
import getEvrImage from '@/assets/getevr_section_header_image.svg'
import initiativesImage from '@/assets/initiatives_section_header_image.svg'

export default defineComponent({
  name: 'LandingSectionLearnMore',
  props: {
    reverse: {
      // type: Boolean,
      default: false
    },
    backgroundImageName: {
      type: String,
      required: true
    }
  },
  setup(props) {
    const router = useRouter()

    const learnMoreItems = ref([
      {
        image: projectsImage,
        text: 'Projects',
        link: '/projects'
      },
      {
        image: miningImage,
        text: 'Mining',
        link: '/mine'
      },
      {
        image: getEvrImage,
        text: 'Get EVR',
        link: '/get_evr'
      },
      {
        image: initiativesImage,
        text: 'Initiatives',
        link: '/initiatives'
      }
    ])

    const displayedItems = computed(() => learnMoreItems.value.slice(0, 4))

    const backgroundImageComputed = computed(() => {
      return new URL(`/src/assets/landing_sections/${props.backgroundImageName}`, import.meta.url)
        .href
    })

    const handleClick = (link: string) => {
      if (link) {
        router.push(link)
      }
    }

    return {
      displayedItems,
      handleClick,
      backgroundImageComputed
    }
  }
})
</script>

<template>
  <section class="learnmore-section">
    <v-container>
      <h2 class="section-title">Learn More</h2>
      <v-container variant="text" class="learnmore-content">
        <v-row class="card-row">
          <v-col
            cols="12"
            xs="6"
            sm="6"
            md="3"
            lg="3"
            xl="3"
            v-for="(item, index) in displayedItems"
            :key="index"
            @click="handleClick(item.link)"
            class="card-col"
          >
            <div class="image-container">
              <img v-if="item.image" :src="item.image" :alt="item.text" class="card-image" />
            </div>
            <p class="card-title">{{ item.text }}</p>
          </v-col>
        </v-row>
      </v-container>
    </v-container>
  </section>
</template>

<style scoped lang="scss">
.learnmore-section {
  height: 730px;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 2rem;
  padding-top: 4rem;
  background-image: url('@/assets/landing_sections/landing_section_94.png');
  background-size: cover;
  background-position: center;

  .section-title {
    font-family: 'Futura', sans-serif;
    font-size: 3rem;
    font-weight: bold;
    color: #ffffff;
    text-align: center;
    margin-bottom: 2rem;
  }

  .learnmore-content {
    max-width: 960px;
  }

  .card-row {
    width: 100%;
    margin: 0;
  }

  .card-col {
    display: flex;
    flex-direction: column;
    align-items: center;
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

  .image-container {
    width: 160px;
    height: 160px;
    border-radius: 50%;
    background-color: #b0b5b8;
    display: flex;
    justify-content: center;
    align-items: center;
    overflow: hidden;
  }

  .card-image {
    width: 70%;
    height: 70%;
    object-fit: contain;
  }

  .card-title {
    font-family: 'Roboto', sans-serif;
    font-size: 1.5rem;
    font-weight: 400;
    line-height: 1.6;
    color: #ffffff;
    opacity: 0.87;
    text-align: center;
  }
}

@media (max-width: 1279px) {
  .learnmore-section {
    height: auto;

    .image-container {
      width: 120px;
      height: 120px;
    }
  }
}

@media (max-width: 959px) {
  .learnmore-section {
    .section-title {
      font-size: 2rem;
      margin-bottom: 1.5rem;
    }

    .learnmore-content {
      max-width: 600px;
    }

    .card-title {
      font-size: 1.25rem;
    }
  }
}

@media (max-width: 599px) {
  .learnmore-section {
    padding-top: 8rem;

    .section-title {
      font-size: 1.75rem;
      margin-bottom: 1rem;
    }

    .learnmore-content {
      max-width: 320px;
    }

    .image-container {
      width: 100px;
      height: 100px;
    }

    .card-title {
      font-size: 1rem;
    }
  }
}
</style>
