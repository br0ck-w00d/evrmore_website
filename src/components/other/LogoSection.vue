<script setup lang="ts">
import { ref } from 'vue'
import logoPackImage from '@/assets/logo_pack/logo_pack.svg'

const resourceItems = ref([
  {
    text: 'Logo Pack',
    image: logoPackImage,
    url: 'https://github.com/br0ck-w00d/Evrmore-Branding-Kit/tree/master/Evrmore_Logos'
  }
])
</script>

<template>
  <section class="logo-section">
    <v-container>
      <h2 class="section-title">Grab the Logo</h2>
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
.logo-section {
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
    margin-bottom: 2rem;
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
  .logo-section {
    height: auto;
    min-height: 450px;
    padding: 4rem 0;

    .section-title {
      font-size: 2rem;
      margin-bottom: 1.5rem;
    }

    .resource-image {
      width: 120px;
      height: 120px;
      margin-bottom: 10px;
    }
  }
}

@media (max-width: 599px) {
  .logo-section {
    .section-title {
      font-size: 1.75rem;
      margin-bottom: 1rem;
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
