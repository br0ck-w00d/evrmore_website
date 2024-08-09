<script lang="ts">
import { defineComponent, ref } from 'vue'
import legalLetterImage from '@/assets/legal_letter.svg'

export default defineComponent({
  name: 'LegalLetterSection',
  setup() {
    const resourceItems = ref([
      {
        text: 'Learn More',
        image: legalLetterImage,
        url: 'https://discord.com/channels/898915073110720542/1265478739181961227/1265788741029597298'
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
  <section class="legalletter-section">
    <v-container>
      <div class="section-title text-center">
        <h2>Legal Letter</h2>
        <p>Evrmore Legal Opinion</p>
      </div>
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
          class="card-col"
        >
          <a :href="item.url">
            <img v-if="item.image" :src="item.image" :alt="item.text" class="resource-image" />
          </a>
          <p class="resource-text">{{ item.text }}</p>
        </v-col>
      </v-row>
    </v-container>
  </section>
</template>

<style scoped lang="scss">
.legalletter-section {
  height: 450px;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;

  .section-title {
    margin-bottom: 2rem;

    h2 {
      font-family: 'Futura', sans-serif;
      font-size: 3rem;
      font-weight: bold;
      margin-bottom: 0.25rem;
    }

    p {
      font-family: 'Roboto', sans-serif;
      font-size: 1.25rem;
      font-weight: 400;
      line-height: 1.6;
      opacity: 0.67;
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
  .legalletter-section {
    height: auto;
    min-height: 650px;
    padding: 4rem 0;

    .section-title {
      h2 {
        font-size: 2rem;
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
  .legalletter-section {
    .section-title {
      h2 {
        font-size: 1.75rem;
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
