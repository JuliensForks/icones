<script setup lang='ts'>
import { pushRecent, setCurrentCollection, useCurrentCollection } from '../../store'

const props = defineProps<{
  id: string
}>()

watch(
  () => props.id,
  () => setCurrentCollection(props.id),
  { immediate: true },
)

onUnmounted(() => setCurrentCollection(''))

const collection = useCurrentCollection()

onMounted(() => {
  pushRecent(props.id)
})
</script>

<template>
  <WithNavbar v-if="!collection">
    <div class="py-8 px-4 text-gray-700 text-center dark:text-dark-700">
      Loading...
    </div>
  </WithNavbar>
  <IconSet v-else :collection="collection" />
</template>
