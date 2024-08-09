<script lang="ts">
import { defineComponent, ref } from 'vue'
import electrumImage from '@/assets/wallets/electrum.svg'
import coreImage from '@/assets/evrmore_logo.svg'
import websiteImage from '@/assets/website.svg'

export default defineComponent({
  name: 'CodeSection',
  setup() {
    const resourceItems = ref([
      {
        text: 'Core',
        image: coreImage,
        url: 'https://github.com/EvrmoreOrg/Evrmore'
      },
      {
        text: 'Electrum',
        image: electrumImage,
        url: 'https://github.com/EvrmoreOrg/electrum-evrmore'
      },
      {
        text: 'Website',
        image: websiteImage,
        url: 'https://github.com/br0ck-w00d/evrmore_website'
      }
    ])

    const handleClick = (url: string) => {
      window.open(url, '_blank')
    }

    return { resourceItems, handleClick }
  }
})
</script>

<template>
  <section class="code-section">
    <v-container>
      <h2 class="section-title">Github Repos</h2>
      <v-container>
        <v-row class="card-row">
          <v-col
            cols="12"
            xs="12"
            sm="12"
            md="3"
            lg="2"
            xl="2"
            v-for="(item, index) in resourceItems"
            :key="index"
            @click="handleClick(item.url)"
            class="card-col"
          >
            <img v-if="item.image" :src="item.image" :alt="item.text" class="resource-image" />
            <p class="resource-text">{{ item.text }}</p>
          </v-col>
        </v-row>
      </v-container>
    </v-container>
  </section>
</template>

<style scoped lang="scss">
.code-section {
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
    font-size: 2.5rem;
    font-weight: bold;
    color: #000000;
    text-align: center;

    &.with-subtitle {
      margin-bottom: 0.2rem;
    }
  }

  .card-row {
    max-width: 1200px;
    display: flex;
    align-items: start;
    justify-content: center;
    margin: 0 auto;
  }

  .card-col {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    transition: transform 0.2s ease;

    &:hover {
      transform: scale(1.05);
    }

    &:active {
      transform: scale(0.95);
    }
  }

  .resource-image {
    width: 160px;
    height: 160px;
    margin-bottom: 10px;
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
  .code-section {
    height: auto;
    min-height: 650px;
    padding: 4rem 0;

    .section-title {
      font-size: 2rem;

      &.with-subtitle {
        margin-bottom: 0.75rem;
      }
    }

    .resource-image {
      width: 120px;
      height: 120px;
      margin-bottom: 10px;
    }
  }
}

@media (max-width: 599px) {
  .code-section {
    .section-title {
      font-size: 1.75rem;

      &.with-subtitle {
        margin-bottom: 0.5rem;
      }
    }

    .resource-image {
      width: 100px;
      height: 100px;
    }

    .resource-text {
      font-size: 0.9rem;
    }
  }
}
</style>
