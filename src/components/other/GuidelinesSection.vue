<script lang="ts">
import { defineComponent, ref } from 'vue'

interface StatItem {
  heading: string
  colors?: string[]
  text?: string
  detail?: string[]
}

export default defineComponent({
  name: 'GuidelinesSection',
  setup() {
    const statItems = ref<StatItem[]>([
      {
        heading: 'Color Palette',
        colors: ['#6ADDFF', '#06C6FF', '#F8F8F8']
      },
      {
        heading: 'Typography',
        text: 'Font Family: Nunito'
      }
    ])

    const copiedColor = ref<string | null>(null)

    const copyColor = (color: string) => {
      navigator.clipboard
        .writeText(color)
        .then(() => {
          copiedColor.value = color
          setTimeout(() => {
            copiedColor.value = null
          }, 2000)
        })
        .catch((err) => {
          console.error('Failed to copy color code:', err)
        })
    }

    return { statItems, copyColor, copiedColor }
  }
})
</script>

<template>
  <section class="guidelines-section">
    <v-container class="h-100 d-flex flex-column align-center justify-center" fluid>
      <h2 class="section-title">Guidelines</h2>
      <v-container fluid>
        <v-row class="card-row">
          <v-col
            cols="12"
            xs="12"
            sm="12"
            md="3"
            lg="3"
            xl="3"
            v-for="(item, index) in statItems"
            :key="index"
            class="card-col"
          >
            <h3 class="stat-heading">{{ item.heading }}</h3>
            <div v-if="item.colors" class="color-circles">
              <div
                v-for="(color, colorIndex) in item.colors"
                :key="colorIndex"
                class="color-circle"
                :style="{ backgroundColor: color }"
                @click="copyColor(color)"
                :title="color"
              >
                <span v-if="copiedColor === color" class="copied-indicator">Copied!</span>
              </div>
            </div>
            <p v-if="item.text" class="stat-text">{{ item.text }}</p>
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
.guidelines-section {
  height: 450px;
  width: 100%;
  display: flex;
  align-items: center;

  .section-title {
    font-family: 'Futura', sans-serif;
    font-size: 2.5rem;
    font-weight: bold;
    color: #000000;
    text-align: center;
    margin-bottom: 1rem;
  }

  .card-row {
    max-width: 750px;
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

  .color-circles {
    display: flex;
    justify-content: center;
    gap: 1rem;
    margin-top: 0.5rem;
  }

  .color-circle {
    width: 30px;
    height: 30px;
    border-radius: 50%;
    cursor: pointer;
    transition: transform 0.2s;
    position: relative;

    &:hover {
      transform: scale(1.1);
    }

    .copied-indicator {
      position: absolute;
      top: -25px;
      left: 50%;
      transform: translateX(-50%);
      background-color: rgba(0, 0, 0, 0.7);
      color: white;
      padding: 2px 6px;
      border-radius: 4px;
      font-size: 0.8rem;
      white-space: nowrap;
    }
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
      justify-content: center;
      align-items: center;
    }

    .section-title {
      font-size: 2rem;
    }

    .stats-grid {
      flex-direction: column;
      gap: 1.5rem;
      align-items: center;
    }

    .stat-item {
      width: 100%;
      max-width: 300px;
    }
  }
}

@media (max-width: 600px) {
  .landing-section {
    .section-title {
      font-size: 1.75rem;
      margin-bottom: 0.5rem;
    }

    .stats-grid {
      gap: 1rem;
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

    .stat-item {
      max-width: 250px;
    }
  }
}
</style>
