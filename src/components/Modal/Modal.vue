<script setup lang="ts">
import { onMounted, onBeforeUnmount, Teleport } from "vue";
import { Card } from "../Card";

interface CardProps {
  isClickOutside: boolean;
}

const props = withDefaults(defineProps<CardProps>(), {
  isClickOutside: false,
});

const emit = defineEmits<{
  (e: "close"): void;
}>();

const handleClickCloseBtn = () => {
  emit("close");
};

const handleClickOutSide = () => {
  if (props.isClickOutside) emit("close");
};

onMounted(() => {
  document.body.style.overflow = "hidden";
});

onBeforeUnmount(() => {
  document.body.style.overflow = "visible";
});
</script>

<template>
  <Teleport to="body">
    <div
      z-50
      fixed
      flex
      items-center
      justify-center
      pa1
      top-0
      left-0
      h-screen
      w-screen
      touch-none
      :style="{
        backgroundColor: `rgba(0, 0, 0, 0.5)`,
      }"
      @click="handleClickOutSide"
    >
      <div z-60 relative>
        <Card w-300px>
          <slot />
        </Card>
        <span
          absolute
          top="-10px"
          right="-5px"
          rounded-full
          border="1px solid #ccc"
          bg-white
          flex
          items-center
          justify-center
          h-25px
          w-25px
          cursor="pointer"
          outline-none
          @click="handleClickCloseBtn"
        >
          X
        </span>
      </div>
    </div>
  </Teleport>
</template>

<style scoped></style>
