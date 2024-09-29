<script setup lang="ts">
import type { CustomIcon, FontAwesomePreset } from '@/model/customIcon'
import ClassicPreset from '@/components/settings/presets/ClassicPreset.vue'
import ModernPreset from '@/components/settings/presets/ModernPreset.vue'
import NeoPreset from '@/components/settings/presets/NeoPreset.vue'
import CustomPreset from '@/components/settings/presets/CustomPreset.vue'
import { ref, computed } from 'vue'
import type { VNode, Component } from 'vue'

defineProps<{
  icon: CustomIcon<FontAwesomePreset>
}>()

const presets = {
  Classic: ClassicPreset,
  Modern: ModernPreset,
  Neo: NeoPreset,
  Custom: CustomPreset
} satisfies Record<string, VNode | Component>

const presetKeys = Object.keys(presets) as IconPreset[]
type IconPreset = keyof typeof presets

const selectedPreset = ref<IconPreset>('Neo')
const selectedPresetComponent = computed(() => {
  return presets[selectedPreset.value]
})
</script>

<template>
  <div>
    <label for="presetselector" class="mb-2 block text-sm font-medium text-gray-900 text-white"
      >Select Icon Preset:</label
    >
    <select
      id="presetselector"
      v-model="selectedPreset"
      class="mb-6 block w-full rounded-lg border border-gray-300 border-gray-600 bg-gray-50 bg-gray-700 p-2.5 text-sm text-gray-900 text-white placeholder-gray-400 focus:border-blue-500 focus:border-blue-500 focus:ring-blue-500 focus:ring-blue-500"
    >
      <option v-for="preset in presetKeys" :value="preset" :key="preset">
        {{ preset }}
      </option>
    </select>

    <component :is="selectedPresetComponent" :icon="icon" />
  </div>
</template>
