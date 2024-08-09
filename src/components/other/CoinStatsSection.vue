<script lang="ts">
import { defineComponent, ref } from 'vue'

interface StatItem {
  heading: string
  text: string
  detail?: string[]
}

export default defineComponent({
  name: 'CoinStatsSection',
  setup() {
    const statItems = ref<StatItem[]>([
      {
        heading: 'Max Supply',
        text: '15,369,186,206 EVR'
      },
      {
        heading: 'Current Supply',
        text: '8,123,694,364 EVR'
      },
      {
        heading: 'Block Time',
        text: '1 minute'
      },
      {
        heading: 'Coinbase Reward',
        text: '2778 EVR',
        detail: ['Foundation: 277.8 EVR', 'Miner: 2500.2 EVR']
      },
      {
        heading: 'Halving Interval',
        text: '1,648,776 Blocks',
        detail: ['~3.13 years']
      }
    ])

    return { statItems }
  }
})
</script>

<template>
  <section class="coinstats-section">
    <v-container>
      <h2 class="section-title">Coin Stats</h2>
      <v-container>
        <v-row class="card-row">
          <v-col
            cols="12"
            xs="12"
            sm="12"
            md="4"
            lg="2"
            xl="2"
            v-for="(item, index) in statItems"
            :key="index"
            class="card-col"
          >
            <h3 class="stat-heading">{{ item.heading }}</h3>
            <p class="stat-text">{{ item.text }}</p>
            <template v-if="item.detail">
              <p v-for="(line, lineIndex) in item.detail" :key="lineIndex" class="stat-detail">
                {{ line }}
              </p>
            </template>
          </v-col>
        </v-row>
      </v-container>
    </v-container>
  </section>
</template>

<style scoped lang="scss">
.coinstats-section {
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
    margin-bottom: 4rem;
  }

  .stat-heading {
    font-family: 'Roboto', sans-serif;
    font-size: 1.2rem;
    font-weight: 700;
    margin-bottom: 0.5rem;
  }

  .stat-text {
    font-family: 'Roboto', sans-serif;
    font-size: 1rem;
    font-weight: 500;
    line-height: 1.6;
    opacity: 0.67;
  }

  .stat-detail {
    font-family: 'Roboto', sans-serif;
    font-size: 0.9rem;
    font-weight: 400;
    line-height: 1.4;
    opacity: 0.5;
    margin-top: 0.25rem;
  }
}

@media (max-width: 1279px) {
  .coinstats-section {
    .card-row {
      max-width: 700px;
    }
  }
}

@media (max-width: 959px) {
  .coinstats-section {
    height: auto;
    min-height: 450px;
    padding: 2rem 0;

    .section-title {
      font-size: 2rem;
    }

    .card-col {
      margin-bottom: 0.5rem;
    }
  }
}

@media (max-width: 599px) {
  .coinstats-section {
    .section-title {
      font-size: 1.75rem;
    }

    .card-col {
      margin: 0;
    }

    .stat-heading {
      font-size: 1.1rem;
    }

    .stat-text {
      font-size: 0.9rem;
    }

    .stat-detail {
      font-size: 0.8rem;
    }
  }
}
</style>
