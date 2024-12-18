<script lang="ts">
import { defineComponent } from 'vue'
import BasicButton from '@/components/commons/BasicButton.vue'
import evrmoreLogo from '@/assets/evrmore_logo.svg'

export default defineComponent({
  name: 'LandingSectionTop',
  components: {
    BasicButton
  },
  setup() {
    console.log('LandingSectionTop rendered');
    const handleClick = () => {
      console.log('clicked');
    };
    return { handleClick, evrmoreLogo };
  }
})
</script>

<template>
  <section class="header-section">
    <v-container fluid class="header-wrapper">
      <div class="header-content-wrapper">
        <div>
          <p class="header-title">Layer One</p>
          <p class="header-title">Made Easy</p>
        </div>
        <div>
          <p class="header-subtitle">Contract Hacks? Not Anymore</p>
        </div>
        <div>
          <BasicButton @click="handleClick">
            <p class="header-button">GRAB A WALLET</p>
          </BasicButton>
        </div>
      </div>
      <div class="header-content-wrapper">
        <img :src="evrmoreLogo" alt="Evrmore Logo" class="header-logo" />
      </div>
    </v-container>
  </section>
</template>

<style scoped lang="scss">
.header-section {
  background-image: url('@/assets/landing_sections/header_background.webp');
  background-size: auto 100%;
  background-position: center;
  background-repeat: repeat-x;
  padding: 1rem;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;

  .header-wrapper {
    display: flex;
    align-items: center;
    justify-content: space-evenly;
    max-width: 1200px;

    .header-content-wrapper {
      display: flex;
      gap: 0.5rem;
      flex-direction: column;
      align-items: flex-start;

      .header-title {
        font-size: 2.7rem;
        font-weight: 700;
        color: #fff;
        line-height: 1.2;
      }

      .header-subtitle {
        font-size: 0.9rem;
        font-weight: 400;
        color: #ffffff72;
        line-height: 1.5;
        margin-bottom: 0.5rem;
      }

      .header-button {
        font-weight: 900;
        color: #ffffff;
        line-height: 1.5;
        font-size: 0.8rem;
      }
    }
  }
}

@media screen and (max-width: 1279px) {
  .header-section {
    .header-wrapper {
      justify-content: space-around;
    }
  }
}

@media (max-width: 768px) {
  .header-section {
    .header-wrapper {
      flex-direction: column;
      flex-direction: column-reverse;
      gap: 2rem;

      .header-content-wrapper {
        align-items: center;
        .header-title {
          font-size: 1.7rem;
        }
        .header-subtitle {
          font-size: 0.7rem;
        }
        .header-button {
          font-size: 0.8rem;
        }
      }
    }
  }
}
</style>
