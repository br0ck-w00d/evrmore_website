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
        name: 'Hans',
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
  <section class="team-section">
    <v-container>
      <div class="text-center section-title">
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
  </section>
</template>

<style scoped lang="scss">
.team-section {
  height: 730px;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 6rem 1rem;
  background-image: url('@/assets/landing_sections/landing_section_f8.png');
  background-size: cover;
  background-position: center;

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

  .team-member {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 0 5rem;

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

  .section-image {
    width: 300px;
    height: 300px;
  }
}

@media (max-width: 1279px) {
  .team-section {
    height: auto;

    .section-image {
      width: 250px;
      height: 250px;
    }
  }
}

@media (max-width: 959px) {
  .team-section {
    .section-title {
      h2 {
        font-size: 2rem;
      }

      p {
        font-size: 1.5rem;
      }
    }

    .image-content {
      flex-direction: column;
      gap: 2rem;
    }

    .section-image {
      width: 200px;
      height: 200px;
    }
  }
}

@media (max-width: 599px) {
  .team-section {
    .section-title {
      h2 {
        font-size: 1.75rem;
      }

      p {
        font-size: 1.25rem;
      }
    }
  }
}
</style>
