<script setup lang="ts">
const props = defineProps<{
  src: string;
  alt: string;
}>();
</script>

<template>
  <div h="60%">
    <img
      w-full
      h-full
      object-cover
      :src="props.src"
      :alt="props.alt"
      loading="lazy"
    />
  </div>
</template>
