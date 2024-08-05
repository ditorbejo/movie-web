<script setup>
defineProps(['title', 'year', 'type', 'poster'])
</script>

<template>
  <div class="flex flex-col p-2 bg-[#F8EDE3] gap-4 rounded-2xl">
    <img
      :src="poster"
      class="h-[200px] lg:h-[400px] object-cover lg:object-fill rounded-2xl w-full"
      alt=""
    />

    <div class="flex flex-col p-2 rounded-2xl">
      <div class="py-2">
        <p class="font-bold text-xl line-clamp-2 h-[50px]">{{ title }}</p>
      </div>

      <div class="flex gap-2 flex-col py-5">
        <p class="font-bold uppercase">
          {{ type }}
        </p>
        <p>
          {{ year }}
        </p>
      </div>
    </div>
  </div>
</template>
