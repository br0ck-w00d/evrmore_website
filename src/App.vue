<script setup lang="ts">
import { RouterView } from 'vue-router'
import { VMain } from 'vuetify/components'
import './styles/main.scss'
import { useToolbarStore } from './store/toolbar-store.pinia'

const toolbarStore = useToolbarStore()

const navigateTo = (url: string) => {
  window.location.href = url
}

const infoDocsItems = [
  {
    title: 'Project Overview',
    url: 'https://hans-schmidt.github.io/mastering_evrmore/project_overview.html'
  },
  {
    title: 'Usage Tips',
    url: 'https://hans-schmidt.github.io/mastering_evrmore/usage_tips/usage_tips.html'
  },
  {
    title: 'Current Technical Docs',
    url: 'https://hans-schmidt.github.io/mastering_evrmore/current_tech_docs/current_tech_docs.html'
  },
  {
    title: 'DeFi Roadmap Docs',
    url: 'https://hans-schmidt.github.io/mastering_evrmore/roadmap_tech_docs/roadmap_tech_docs.html'
  },
  { title: 'EVR vs ETH vs EUTXO', url: 'https://evrmorecoin.org/docs/evr-vs-eth-vs-eutxo' },
  {
    title: 'EvrLight and Nostr4Evr',
    url: 'https://hans-schmidt.github.io/mastering_evrmore/evrlight_and_nostr4evr/evrlight_and_nostr4evr.html'
  },
  {
    title: 'Summary Tech Info for Devs',
    url: 'https://hans-schmidt.github.io/mastering_evrmore/Summary_of_Evrmore_Chain_Parameters_for_Developers.html'
  }
]
</script>

<template>
  <v-app class="app-background">
    <div class="toolbar-container">
      <v-toolbar height="56px" density="default" color="transparent">
        <div @click="navigateTo('https://evrmore.com')" class="logo-title-container">
          <img
            src="@/assets/evrmore_logo_thick.svg"
            alt="Evrmore Logo"
            width="24"
            height="24"
            class="ml-4 clickable"
          />
          <v-toolbar-title :style="{ color: toolbarStore.toolbarTextColor }" class="clickable"
            >Evrmore</v-toolbar-title
          >
        </div>
        <v-spacer></v-spacer>
        <v-btn
          @click="navigateTo('https://evrmore.com/get_evr')"
          :color="toolbarStore.toolbarTextColor"
          >Get EVR</v-btn
        >
        <v-btn
          @click="navigateTo('https://evrmore.com/mine')"
          :color="toolbarStore.toolbarTextColor"
          >Mining</v-btn
        >
        <v-btn
          @click="navigateTo('https://evrmore.com/marketing')"
          :color="toolbarStore.toolbarTextColor"
          >Marketing</v-btn
        >
        <v-btn disabled :color="toolbarStore.toolbarTextColor">Build</v-btn>
        <v-btn
          @click="navigateTo('https://evrmore.com/initiatives')"
          :color="toolbarStore.toolbarTextColor"
          >Initiatives</v-btn
        >
        <v-menu
          transition="scale-transition"
          :close-on-content-click="true"
          :nudge-width="200"
          offset="2"
        >
          <template v-slot:activator="{ props }">
            <v-btn v-bind="props" :color="toolbarStore.toolbarTextColor"> Info & Docs </v-btn>
          </template>
          <v-list
            rounded="xl"
            :bg-color="toolbarStore.toolbarTextColor === 'white' ? '#F8F8F8' : '#3A3A3A'"
          >
            <v-list-item
              v-for="(item, index) in infoDocsItems"
              :key="index"
              :value="index"
              @click="navigateTo(item.url)"
              :ripple="false"
            >
              <v-list-item-title
                :style="{
                  color:
                    toolbarStore.toolbarTextColor === 'white'
                      ? 'rgba(0, 0, 0, 0.67)'
                      : 'rgba(255, 255, 255, 0.87)'
                }"
              >
                {{ item.title }}
              </v-list-item-title>
            </v-list-item>
          </v-list>
        </v-menu>
      </v-toolbar>
    </div>
    <v-main>
      <transition name="fade" mode="out-in">
        <RouterView />
      </transition>
    </v-main>
  </v-app>
</template>

<style scoped>
.app-background {
  background-color: #ffffff;
  min-height: 100vh;
  position: relative;
  display: flex;
  flex-direction: column;
}

.toolbar-container {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  z-index: 10;
  display: flex;
  justify-content: center;
}

.v-toolbar {
  width: 100%;
  max-width: 1920px;
  margin: 0 auto;
  padding-top: 1rem;
}

.v-toolbar-title {
  font-family: 'Futura', Sans-serif;
  font-size: 0.875rem;
  margin-inline-start: 1rem;
}

.v-toolbar .v-btn {
  text-transform: none;
  font-size: 0.75rem;
  font-weight: medium;
}

.logo-title-container {
  display: flex;
  align-items: center;
  cursor: pointer;
}

.clickable {
  cursor: pointer;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>

<style scoped>
.app-background {
  background-color: #ffffff;
  min-height: 100vh;
  position: relative;
  display: flex;
  flex-direction: column;
}

.toolbar-container {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  z-index: 10;
  display: flex;
  justify-content: center;
}

.v-toolbar {
  width: 100%;
  max-width: 1920px;
  margin: 0 auto;
  padding-top: 1rem;
}

.v-toolbar-title {
  font-family: 'Futura', Sans-serif;
  font-size: 0.875rem;
  margin-inline-start: 1rem;
}

.v-toolbar .v-btn {
  text-transform: none;
  font-size: 0.75rem;
  font-weight: medium;
}

.logo-title-container {
  display: flex;
  align-items: center;
  cursor: pointer;
}

.clickable {
  cursor: pointer;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

:deep(.v-list-item) {
  min-height: 35px !important;
  padding: 0 16px !important;
}

:deep(.v-list-item__content) {
  padding: 8px 0 !important;
}

:deep(.v-list-item-title) {
  font-size: 14px !important;
  font-weight: 500 !important;
}
</style>
