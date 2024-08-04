<script lang="ts">
import { computed, defineComponent, ref } from 'vue'
import teamImage from '@/assets/team.svg'
import githubImage from '@/assets/socials/github.svg'
import twitterImage from '@/assets/socials/twitter.svg'
import instagramImage from '@/assets/socials/instagram.svg'

export default defineComponent({
  name: 'TeamSection',
  props: {
    backgroundImageName: {
      type: String,
      required: true
    }
  },
  setup(props) {
    const teamInfo = ref({
      image: teamImage,
      alt: 'Team Image'
    })

    const teamMembers = ref([
      {
        name: 'Zeroth',
        socials: [
          { logo: twitterImage, alt: 'Twitter Logo', link: 'https://x.com/br0ck_w00d' },
          { logo: githubImage, alt: 'Github Logo', link: 'https://github.com/br0ck-w00d' },
          { logo: instagramImage, alt: 'Instagram Logo', link: 'https://instagram.com/br0ck_w00d' }
        ]
      },
      {
        name: 'Hans Schmidt',
        socials: [
          { logo: twitterImage, alt: 'Twitter Logo', link: 'https://x.com/Hans_Schm1dt' },
          { logo: githubImage, alt: 'Github Logo', link: 'https://github.com/hans-schmidt' }
          // { logo: instagramImage, alt: 'Instagram Logo', link: 'https://instagram.com/hans' }
        ]
      }
    ])

    const backgroundImageComputed = computed(() => {
      return new URL(`/src/assets/landing_sections/${props.backgroundImageName}`, import.meta.url)
        .href
    })

    const handleClick = (link: string) => {
      if (link) {
        window.open(link, '_blank')
      }
    }

    return { teamInfo, teamMembers, backgroundImageComputed, handleClick }
  }
})
</script>

<template>
  <section class="landing-section team-section">
    <img :src="backgroundImageComputed" alt="Team Background" class="section-background" />
    <div class="content-wrapper">
      <v-container class="d-flex flex-column align-center justify-center h-100">
        <div class="text-content text-center">
          <h2>Team</h2>
          <p>Current & Former Raven Devs, & Hodlers</p>
        </div>
        <div class="image-content">
          <div class="team-member left">
            <div class="circle-stack">
              <div
                v-for="(social, index) in teamMembers[0].socials"
                :key="index"
                class="circle-logo"
                :class="{ 'top-circle': index === 0 }"
                :style="{ zIndex: teamMembers[0].socials.length - index }"
                @click="handleClick(social.link)"
              >
                <img :src="social.logo" :alt="social.alt" />
              </div>
            </div>
            <p class="member-name">{{ teamMembers[0].name }}</p>
          </div>
          <img :src="teamInfo.image" :alt="teamInfo.alt" class="section-image" />
          <div class="team-member right">
            <div class="circle-stack">
              <div
                v-for="(social, index) in teamMembers[1].socials"
                :key="index"
                class="circle-logo"
                :class="{ 'top-circle': index === 0 }"
                :style="{ zIndex: teamMembers[1].socials.length - index }"
                @click="handleClick(social.link)"
              >
                <img :src="social.logo" :alt="social.alt" />
              </div>
            </div>
            <p class="member-name">{{ teamMembers[1].name }}</p>
          </div>
        </div>
      </v-container>
    </div>
  </section>
</template>

<style scoped lang="scss">
.landing-section {
  position: relative;
  height: 730px;
  width: 100%;
  display: flex;
  align-items: center;

  &.team-section {
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
    z-index: 2;
    width: 100%;
    height: 100%;
  }

  .text-content {
    color: #000000;
    max-width: 600px;
    margin-bottom: 2rem;

    h2 {
      font-family: 'Futura', sans-serif;
      font-size: 3rem;
      font-weight: bold;
      margin-bottom: 0.25rem;
    }

    p {
      font-family: 'Roboto', sans-serif;
      font-size: 1.75rem;
      font-weight: 400;
      line-height: 1.6;
      opacity: 0.67;
    }
  }

  .image-content {
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .section-image {
    max-width: 100%;
    height: auto;
    max-height: 390px;
  }

  .team-member {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 0 2rem;

    .circle-stack {
      position: relative;
      width: 130px;
      height: 130px;
      margin-bottom: 1rem;

      &:hover {
        .circle-logo {
          &:nth-child(1) {
            transform: translateY(-45px) scale(1.1);
          }
          &:nth-child(2) {
            transform: translateY(0) scale(1.1);
          }
          &:nth-child(3) {
            transform: translateY(45px) scale(1.1);
          }
        }
      }
    }

    .circle-logo {
      position: absolute;
      top: 5px;
      left: 5px;
      width: 120px;
      height: 120px;
      border-radius: 50%;
      overflow: hidden;
      display: flex;
      justify-content: center;
      align-items: center;
      background-color: #f0f0f0;
      cursor: pointer;
      transition: all 0.3s ease;

      &.top-circle {
        top: 0;
        left: 0;
        width: 130px;
        height: 130px;
      }

      img {
        width: 100%;
        height: 100%;
        object-fit: cover;
      }
    }

    .member-name {
      font-family: 'Roboto', sans-serif;
      font-size: 1.2rem;
      text-align: center;
    }
  }
}

@media (max-width: 960px) {
  .landing-section {
    height: auto;
    min-height: 730px;

    .section-image {
      max-height: 300px;
    }

    .text-content {
      padding-left: 0;
      padding-bottom: 1rem;
      text-align: center;
    }

    .image-content {
      flex-direction: column;
    }

    .team-member {
      margin: 1rem 0;
    }
  }
}
</style>
