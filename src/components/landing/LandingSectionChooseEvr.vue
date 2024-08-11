<script lang="ts">
import { computed, defineComponent, ref } from 'vue'
import bulletProofImage from '@/assets/choose_evr/more_secure.svg'
import layerOneDefiImage from '@/assets/landing_sections/layer_one_defi.svg'
import oneClickFinanceImage from '@/assets/landing_sections/easy_swaps.svg'

export default defineComponent({
  name: 'RebelMissionSection',
  props: {
    backgroundImageName: {
      type: String,
      required: true
    }
  },
  setup(props) {
    const resourceItems = ref([
      {
        text: 'True Layer One',
        image: layerOneDefiImage,
        url: '#'
      },
      {
        text: 'Bulletproof Primitives',
        image: bulletProofImage,
        url: '#'
      },
      {
        text: 'One-Click Finance',
        image: oneClickFinanceImage,
        url: '#'
      }
    ])

    const backgroundImageComputed = computed(() => {
      return new URL(`/src/assets/landing_sections/${props.backgroundImageName}`, import.meta.url)
        .href
    })

    return { resourceItems, backgroundImageComputed }
  }
})
</script>

<template>
  <section class="choose-evr-section">
    <v-container>
      <h2 class="section-title">Rebel Mission</h2>
      <v-container variant="text">
        <v-row class="card-row">
          <v-col
            cols="12"
            xs="12"
            sm="12"
            md="4"
            lg="4"
            xl="3"
            v-for="(item, index) in resourceItems"
            :key="index"
            class="card-col"
          >
            <img v-if="item.image" :src="item.image" :alt="item.text" class="card-image" />
            <p class="card-title">{{ item.text }}</p>
          </v-col>
        </v-row>
      </v-container>
    </v-container>
  </section>
</template>

<style scoped lang="scss">
.choose-evr-section {
  height: 730px;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 2rem;

  .section-title {
    font-family: 'Futura', sans-serif;
    font-size: 3rem;
    font-weight: bold;
    color: #000000;
    text-align: center;
    margin-bottom: 2rem;
  }

  .card-row {
    width: 100%;
    margin: 0;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .card-col {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }

  .card-image {
    width: 300px;
    height: 300px;
    margin-bottom: 1rem;
  }

  .card-title {
    font-family: 'Roboto', sans-serif;
    font-size: 1.75rem;
    font-weight: 400;
    line-height: 1.6;
    opacity: 0.67;
    text-align: center;
  }
}

@media (max-width: 1279px) {
  .choose-evr-section {
    height: auto;

    .card-image {
      width: 250px;
      height: 250px;
    }
  }
}

@media (max-width: 959px) {
  .choose-evr-section {
    .section-title {
      font-size: 2rem;
      margin-bottom: 1.5rem;
    }

    .card-col {
      margin-bottom: 2rem;
    }

    .card-title {
      font-size: 1.5rem;
    }
  }
}

@media (max-width: 599px) {
  .choose-evr-section {
    .section-title {
      font-size: 1.75rem;
      margin-bottom: 1rem;
    }

    .card-col {
      margin-bottom: 1rem;
    }

    .card-image {
      width: 200px;
      height: 200px;
    }

    .card-title {
      font-size: 1.25rem;
    }
  }
}
</style>
