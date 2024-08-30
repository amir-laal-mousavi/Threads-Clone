<template>
  <NuxtLayout>
    <div id="IndexPage" class="w-full overflow-auto">
      <div class="mx-auto overflow-hidden max-w-[500px]">
        <div class="px-4 mx-auto max-w-[600px]" id="Posts">
          <div v-if="isPosts" v-for="post in posts" :key="post">
            <Post :post="post" @isDeleted="post = userStore.getAllPosts()" />
          </div>
          <div v-else>
              <div v-if="isLoading" class="mt-20 w-full flex items-center justify-center mx-auto">
                <div class="text-white mx-auto flex flex-col items-center justify-center">
                  <Icon name="eos-icons:bubble-loading" size="50" color="#fff" />
                  <div class="w-full mt-1">Loading...</div>
                </div>
              </div>
              <div v-if="!isLoading" class="mt-20 w-full flex items-center justify-center mx-auto">
                <div class="text-white mx-auto flex flex-col items-center justify-center">
                  <Icon name="tabler:mood-empty" size="50" color="#fff" />
                  <div class="w-full mt-1">Make the first post!</div>
                </div>
              </div>
          </div>
        </div>
      </div>
    </div>
  </NuxtLayout>
</template>

<script setup>

import { useUserStore } from '~/stores/user';
const userStore = useUserStore()
const user = useSupabaseUser()

let posts = ref([])
let isPosts = ref(false)
let isLoading = ref(false)



onBeforeMount(async () => {
  try {
    isLoading.value = true;
    await userStore.getAllPosts();
    isLoading.value = false;
  } catch (error) {
    console.log(error,"im here");
  }
})


onMounted(() => {
  watchEffect(() => {
    if (userStore.posts && userStore.posts.length >= 0) {
      posts.value = userStore.posts
      isPosts.value = true
    } else {
      isPosts.value = false;
    }
  })

  watchEffect(() => {
  if (!user.value) {
    return navigateTo('/auth')
  }
})
})

watch(() => posts.value, () => {
  if (userStore.posts && userStore.posts.length <= 0) {
    posts.value = userStore.posts
    isPosts.value = true
  }
}, { deep: true }) // watching inside the object so if can find any changes

</script>

