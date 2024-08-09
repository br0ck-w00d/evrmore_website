<script lang="ts">
import { computed, defineComponent, ref } from 'vue'
import xeggexImage from '@/assets/exchanges/xeggex.svg'
import coinWImage from '@/assets/exchanges/coinw.svg'
import safeTradeImage from '@/assets/exchanges/safetrade.svg'

export default defineComponent({
  name: 'ExchangesSection',
  props: {
    backgroundImageName: {
      type: String,
      required: true
    }
  },
  setup(props) {
    const resourceItems = ref([
      {
        text: 'Xeggex',
        image: xeggexImage,
        url: 'https://xeggex.com/market/EVR_USDT'
      },
      {
        text: 'CoinW: Get Involved',
        image: coinWImage,
        url: 'https://discord.com/channels/898915073110720542/1253304077845266483/1253367435676094545'
      },
      {
        text: 'SafeTrade',
        image: safeTradeImage,
        url: 'https://safetrade.com/exchange/EVR-USDT?type=basic'
      }
    ])

    const backgroundImageComputed = computed(() => {
      return new URL(`/src/assets/landing_sections/${props.backgroundImageName}`, import.meta.url)
        .href
    })

    const handleClick = (url: string) => {
      window.open(url, '_blank')
    }

    return { resourceItems, backgroundImageComputed, handleClick }
  }
})
</script>

<template>
  <section class="exchanges-section">
    <v-container>
      <h2 class="section-title">Exchanges</h2>
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
            <img v-if="item.image" :src="item.image" :alt="item.text" class="exchanges-image" />
            <p class="exchanges-text">{{ item.text }}</p>
          </v-col>
        </v-row>
      </v-container>
    </v-container>
  </section>
</template>

<style scoped lang="scss">
.exchanges-section {
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

  .exchanges-image {
    width: 160px;
    height: 160px;
    margin-bottom: 10px;
  }

  .exchanges-text {
    font-family: 'Roboto', sans-serif;
    font-size: 1rem;
    font-weight: 500;
    line-height: 1.6;
    opacity: 0.67;
    text-align: center;
  }
}

@media (max-width: 959px) {
  .exchanges-section {
    height: auto;
    min-height: 450px;
    padding: 4rem 0;

    .section-title {
      font-size: 2rem;

      &.with-subtitle {
        margin-bottom: 0.75rem;
      }
    }

    .exchanges-image {
      width: 120px;
      height: 120px;
      margin-bottom: 10px;
    }
  }
}

@media (max-width: 599px) {
  .exchanges-section {
    .section-title {
      font-size: 1.75rem;

      &.with-subtitle {
        margin-bottom: 0.5rem;
      }
    }

    .exchanges-image {
      width: 100px;
      height: 100px;
    }

    .exchanges-text {
      font-size: 0.9rem;
    }
  }
}
</style>
