<script lang="ts">
import { computed, defineComponent, ref } from 'vue'
import { useRouter } from 'vue-router'
import projectsImage from '@/assets/projects/projects.svg'
import miningImage from '@/assets/mining/mining_section_header_image.svg'
import getEvrImage from '@/assets/getevr_section_header_image.svg'
import initiativesImage from '@/assets/initiatives_section_header_image.svg'
import marketingImage from '@/assets/marketing_section_header_image.svg'
import infoDocsImage from '@/assets/info&docs.svg'
import communityImage from '@/assets/socials/community.svg'
import developmentImage from '@/assets/landing_sections/development.svg'

export default defineComponent({
  name: 'LandingSectionLearnMore',
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
    const router = useRouter()

    const learnMoreItems = ref([
      {
        image: projectsImage,
        text: 'Projects',
        link: '#' // TODO: Create View and update link
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
      },
      {
        image: marketingImage,
        text: 'Marketing',
        link: '/marketing'
      },
      {
        image: infoDocsImage,
        text: 'Info & Docs',
        link: '#' // TODO: Create View and update link
      },
      {
        image: communityImage,
        text: 'Community',
        link: '#' // TODO: Create View and update link
      },
      {
        image: developmentImage,
        text: 'Development',
        link: '#' // TODO: Create View and update link
      }
    ])

    const backgroundImageComputed = computed(() => {
      return new URL(`/src/assets/landing_sections/${props.backgroundImageName}`, import.meta.url)
        .href
    })

    const handleClick = (link: string) => {
      if (link) {
        router.push(link)
      }
    }

    const currentPage = ref(0)
    const itemsPerPage = 4

    const totalPages = computed(() => Math.ceil(learnMoreItems.value.length / itemsPerPage))

    const nextPage = () => {
      currentPage.value = (currentPage.value + 1) % totalPages.value
    }

    const prevPage = () => {
      currentPage.value = (currentPage.value - 1 + totalPages.value) % totalPages.value
    }

    return {
      learnMoreItems,
      handleClick,
      backgroundImageComputed,
      currentPage,
      nextPage,
      prevPage,
      itemsPerPage,
      totalPages
    }
  }
})
</script>

<template>
  <section class="landing-section landing-section-learn-more" :class="{ reverse: reverse }">
    <img :src="backgroundImageComputed" alt="Section Background" class="section-background" />
    <div class="content-wrapper">
      <v-container class="d-flex flex-column align-center justify-center h-100">
        <div class="text-content text-center">
          <h2>Learn More</h2>
        </div>
        <div class="learn-more-carousel">
          <v-btn icon @click="prevPage" class="carousel-nav left" color="#6D7378">
            <v-icon color="white" size="32">mdi-chevron-left</v-icon>
          </v-btn>
          <div class="learn-more-window">
            <v-window v-model="currentPage" class="learn-more-window-inner">
              <v-window-item v-for="n in totalPages" :key="n">
                <div class="learn-more-grid">
                  <div
                    v-for="(item, index) in learnMoreItems.slice(
                      (n - 1) * itemsPerPage,
                      n * itemsPerPage
                    )"
                    :key="index"
                    class="learn-more-item"
                    @click="handleClick(item.link)"
                  >
                    <div class="circle-container">
                      <img :src="item.image" :alt="item.text" class="learn-more-image" />
                    </div>
                    <div class="learn-more-content">
                      <p class="learn-more-title">{{ item.text }}</p>
                    </div>
                  </div>
                </div>
              </v-window-item>
            </v-window>
          </div>
          <v-btn icon @click="nextPage" class="carousel-nav right" color="#6D7378">
            <v-icon color="white" size="32">mdi-chevron-right</v-icon>
          </v-btn>
        </div>
      </v-container>
    </div>
  </section>
</template>

<style scoped lang="scss">
.landing-section {
  position: relative;
  height: 600px;
  width: 100%;
  display: flex;
  align-items: center;

  &.landing-section-learn-more {
    z-index: 3;
    margin-top: -120px;
  }

  .section-background {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  .content-wrapper {
    position: relative;
    z-index: 3;
    width: 100%;
    height: 100%;
  }

  .text-content {
    color: #000000;
    max-width: 600px;
    text-align: center;

    h2 {
      font-family: 'Futura', sans-serif;
      font-size: 2rem;
      font-weight: bold;
      color: #ffffff;
      margin-bottom: 0.25rem;
    }
  }

  .learn-more-carousel {
    position: relative;
    width: 100%;
    max-width: 960px;
    margin: 0 auto;
    display: flex;
    align-items: flex-start;
    overflow: visible;
  }

  .learn-more-window {
    width: 100%;
    overflow: hidden;
    padding: 2rem 0;
  }

  .learn-more-window-inner {
    overflow: visible;
  }

  .learn-more-grid {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: flex-start;
    gap: 2.25rem;
  }

  .carousel-nav {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    z-index: 1;

    &.left {
      left: -20px;
    }

    &.right {
      right: -20px;
    }
  }

  .learn-more-item {
    display: flex;
    flex-direction: column;
    align-items: center;
    cursor: pointer;
    transition:
      transform 0.2s ease,
      opacity 0.3s ease;
    width: 100%;
    max-width: 160px;

    &:hover {
      transform: scale(1.05);
      z-index: 1;
    }

    &:active {
      transform: scale(0.95);
    }
  }

  .circle-container {
    width: 120px;
    height: 120px;
    border-radius: 50%;
    background-color: #b0b5b8;
    display: flex;
    justify-content: center;
    align-items: center;
    overflow: hidden;
    margin-bottom: 1rem;
  }

  .learn-more-image {
    max-width: 80%;
    max-height: 80%;
    object-fit: contain;
  }

  .learn-more-content {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 100%;
  }

  .learn-more-title {
    font-family: 'Roboto', sans-serif;
    font-size: 1.25rem;
    font-weight: 500;
    text-align: center;
    margin: 0;
    color: #ffffff;
    opacity: 0.87;
  }
}

@media (max-width: 959px) {
  .landing-section {
    height: auto;
    min-height: 730px;
    padding: 2rem 0;

    .content-wrapper {
      display: flex;
      flex-direction: column;
      justify-content: flex-start;
      align-items: center;
    }

    .text-content {
      padding: 2rem;

      h2 {
        font-size: 2rem;
      }
    }

    .learn-more-grid {
      flex-wrap: wrap;
      gap: 1.25rem;
    }

    .circle-container {
      width: 120px;
      height: 120px;
    }

    .learn-more-title {
      font-size: 1.25rem;
    }
  }
}

@media (max-width: 599px) {
  .landing-section {
    .text-content {
      padding: 1rem;

      h2 {
        font-size: 1.75rem;
      }
    }

    .learn-more-grid {
      gap: 1rem;
    }

    .circle-container {
      width: 100px;
      height: 100px;
    }

    .learn-more-title {
      font-size: 1rem;
    }
  }
}
</style>
