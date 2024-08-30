<template>
  <div id="MainLayout" class="h-screen">
    <div class="w-full max-w-[500px] mx-auto">
      <div class="w-full flex items-center justify-center px-2 h-10 my-2" id="TopMenu">
        <img src="/threads-logo.png" alt="logo" class="w-[35px]">
      </div>
    </div>
    <div class="flex w-full mx-auto h-screen max-w-[500px]">
      <slot />
    </div>

    <div
      id="BottomNav"
      class="fixed z-50 bottom-0 flex w-full h-[70px] border-t border-t-gray-700 bg-black">
      <div class="w-full max-w-[500px] mx-auto flex items-center justify-around">
        <button 
          class="w-full h-full text-white"
          @click="navigateTo('/')">
          <Icon name="material-symbols:home-outline" color="#ffffff" size="35" />
        </button>
        <button
          @click="userStore.isMenuOverlay = true"
          class="w-full h-full text-white">
          <Icon name="material-symbols:edit-square-outline-rounded" class="mb-1" color="#fff" size="32" />
        </button>
        <button
          @click="userStore.isLogoutOverlay = true"
          class="w-full h-full text-white">
          <Icon name="ph:sign-out" class="mb-1" color="#fff" size="32" />
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { useUserStore } from '~/stores/user';
const userStore = useUserStore()
</script>
