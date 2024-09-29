<script setup lang="ts">
import { reactive } from 'vue'
import type { CustomIcon, FontAwesomePreset } from '@/model/customIcon'

const props = defineProps<{
  icon: CustomIcon<FontAwesomePreset>
}>()

const currentIcon = reactive(props.icon ?? ({} as CustomIcon<FontAwesomePreset>))
currentIcon.presetSettings = {
  preset: 'Modern',
  inverted: false
}
currentIcon.fontAwesomeIcon.style = 'thin'
currentIcon.fontAwesomeIcon.family = 'sharp'
</script>

<template>
  <label class="inline-flex cursor-pointer items-center">
    <input
      type="checkbox"
      class="peer sr-only"
      v-model="(currentIcon as CustomIcon<'Modern'>).presetSettings.inverted"
    />
    <div
      class="peer relative h-6 w-11 rounded-full border-gray-600 bg-gray-200 bg-gray-700 after:absolute after:start-[2px] after:top-[2px] after:h-5 after:w-5 after:rounded-full after:border after:border-gray-300 after:bg-white after:transition-all after:content-[''] peer-checked:bg-blue-600 peer-checked:after:translate-x-full peer-checked:after:border-white peer-focus:outline-none peer-focus:ring-4 peer-focus:ring-blue-300 peer-focus:ring-blue-800 rtl:peer-checked:after:-translate-x-full"
    ></div>
    <span class="ms-3 text-sm font-medium text-gray-900 text-white">Invert Colors</span>
  </label>
</template>

<style scoped></style>
