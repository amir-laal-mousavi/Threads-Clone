<template>
  <div id="AuthPage" class="w-full h-[100vh] h-screen pt-32">
    <div class="w-full">
      <div class="w-full flex items-center justify-center gap-2 5 p-2">
        <img src="/threads-logo.png" class="w-[35px]">
        <span class="font-bold text-2xl text-white">
          Threads
        </span>
      </div>

      <div class="max-w-[350px] mx-auto px-2 text-white">
        <div class="text-center mb-6 mt-4">Login / Register</div>

        <button
          @click="login('github')"
          class="
            flex
            items-center
            justify-center
            gap-3
            p-1.5
            w-full
            border
            rounded-full
            text-lg
            font-semibold
          ">
          <div class="flex items-center gap-2 justify-center">
            <img src="/github-logo.png" class="w-full max-w-[30px] rounded-full">
            Github
          </div>
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
const client = useSupabaseClient()
const user = useSupabaseUser()

watchEffect(() => {
  if (user.value) {
    return navigateTo('/')
  }
})

const login = async (prov) => {
  const { data, error } = await client.auth.signInWithOAuth({
    provider: prov,
    redirectTo: window.location.origin
  })
  
  if (error) console.log(error + 'im here bitch');
  
}

</script>
