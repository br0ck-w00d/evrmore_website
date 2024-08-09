<script lang="ts">
import { defineComponent, ref } from 'vue'
import magicImage from '@/assets/wallets/magic.svg'
import electrumImage from '@/assets/wallets/electrum.svg'
import coreImage from '@/assets/evrmore_logo.svg'

export default defineComponent({
  name: 'WalletSection',
  setup() {
    const resourceItems = ref([
      {
        text: 'Magic',
        image: magicImage,
        url: 'https://twitter.com/magicwalletapp'
      },
      {
        text: 'Electrum',
        image: electrumImage,
        url: 'https://github.com/EvrmoreOrg/electrum-evrmore/releases'
      },
      {
        text: 'Core',
        image: coreImage,
        url: 'https://github.com/EvrmoreOrg/Evrmore/releases/tag/v1.0.5'
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
  <section class="wallets-section">
    <v-container>
      <h2 class="section-title">Wallets</h2>
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
            <img v-if="item.image" :src="item.image" :alt="item.text" class="wallet-image" />
            <p class="wallet-text">{{ item.text }}</p>
          </v-col>
        </v-row>
      </v-container>
    </v-container>
  </section>
</template>

<style scoped lang="scss">
.wallets-section {
  height: 450px;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;

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

  .wallet-image {
    width: 160px;
    height: 160px;
    margin-bottom: 10px;
  }

  .wallet-text {
    font-family: 'Roboto', sans-serif;
    font-size: 1rem;
    font-weight: 500;
    line-height: 1.6;
    opacity: 0.67;
    text-align: center;
  }
}

@media (max-width: 959px) {
  .wallets-section {
    height: auto;
    min-height: 450px;
    padding: 4rem 0;

    .section-title {
      font-size: 2rem;

      &.with-subtitle {
        margin-bottom: 0.75rem;
      }
    }

    .wallet-image {
      width: 120px;
      height: 120px;
      margin-bottom: 10px;
    }
  }
}

@media (max-width: 599px) {
  .resoucres-section {
    .section-title {
      font-size: 1.75rem;

      &.with-subtitle {
        margin-bottom: 0.5rem;
      }
    }

    .wallet-image {
      width: 100px;
      height: 100px;
    }

    .wallet-text {
      font-size: 0.9rem;
    }
  }
}
</style>
