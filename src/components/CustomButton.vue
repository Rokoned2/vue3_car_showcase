<template>
  <button
    :disabled="isDisabled"
    :type="btnType || 'button'"
    class="custom-btn"
    :class="containerStyles"
    @click="$emit('handleClick')"
  >
    <span class="flex-1" :class="textStyles">{{ title }}</span>

    <div v-if="rightIcon" className="relative w-6 h-6">
      <img :src="rightIcon" alt="arrow_left" className="object-contain" />
    </div>
  </button>
</template>

<script setup>
const props = defineProps([
  "isDisabled",
  "btnType",
  "containerStyles",
  "textStyles",
  "title",
  "rightIcon",
]);
const emit = defineEmits(["handleClick"]);
</script>
