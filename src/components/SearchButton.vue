<template>
  <button type="submit" class="-ml-3 z-10" :class="otherClasses">
    <img
      :src="magnifyingGlass"
      alt="magnifying glass"
      width="40"
      height="40"
      className="object-contain"
    />
  </button>
</template>

<script setup>
const magnifyingGlass =
  import.meta.env.BASE_URL + "src/assets/magnifying-glass.svg";
const props = defineProps(["otherClasses"]);
</script>
