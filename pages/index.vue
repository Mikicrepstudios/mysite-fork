<template>
  <div class="max-w-2xl mx-auto space-y-4 md:space-y-6 relative z-10">
    <GridBackground />
    <div class="border border-white/5 rounded-lg p-4 md:p-6 bg-black/50 backdrop-blur-xl backdrop-saturate-150 relative">
      <div class="flex flex-col items-center text-center space-y-4 md:space-y-6">
        <div class="relative w-16 h-16 md:w-24 md:h-24">
          <img src="https://x.spitkov.hu/u/aMSOMT.png" alt="Profile Picture" class="w-full h-full rounded-xl object-cover" />
          <div :class="['absolute -bottom-1 -right-1 w-3 h-3 md:w-4 md:h-4 rounded-full border-2 border-black', statusColor]"></div>
        </div>
        
        <div class="space-y-4">
          <div class="font-bold text-xl">spitkov</div>
          <div class="space-y-2">
            <p class="text-white/90">full-stack dev - cybersec</p>
            <p class="text-white/90">Hungary</p>
            <div class="flex justify-center space-x-4 text-white/70 hover:text-white/90">
              <a href="mailto:hello@spitkov.hu" class="hover:text-white hover:underline transition-colors">email</a>
              <span>•</span>
              <a href="https://github.com/spitkov" target="_blank" class="hover:text-white hover:underline transition-colors">github</a>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="border border-white/5 rounded-lg p-4 md:p-6 bg-black/50 backdrop-blur-xl backdrop-saturate-150 relative">
      <div class="font-bold text-xl mb-4">Discord Status</div>
      <DiscordStatus />
    </div>
  </div>
</template>

<script setup>
const { data: discordData } = await useFetch(`https://api.lanyard.rest/v1/users/${useRuntimeConfig().public.discordId}`)

const statusColor = computed(() => {
  if (!discordData.value?.data?.discord_status) return 'bg-white/20'
  switch (discordData.value.data.discord_status) {
    case 'online': return 'bg-[#43b581]'
    case 'idle': return 'bg-[#faa61a]'
    case 'dnd': return 'bg-[#f04747]'
    default: return 'bg-[#747f8d]'
  }
})
</script> 