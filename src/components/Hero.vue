<template>
  <div class="hero">
    <div class="flex-1 pt-36 padding-x">
      <h1 class="hero__title">Find, book, rent a car—quick and super easy!</h1>

      <p class="hero__subtitle">
        Streamline your car rental experience with our effortless booking
        process.
      </p>

      <CustomButton
        title="Explore Cars"
        containerStyles="bg-primary-blue text-white rounded-full mt-10"
        @handleClick="handleScroll"
      />
    </div>
    <div class="hero__image-container">
      <div class="hero__image">
        <img :src="heroImage" alt="hero" class="object-contain fill" />
      </div>

      <div class="hero__image-overlay" />
    </div>
  </div>
</template>

<script setup>
import CustomButton from "./CustomButton.vue";

const heroImage = import.meta.env.BASE_URL + "src/assets/hero.png";

const handleScroll = () => {
  const nextSection = document.getElementById("discover");
  if (nextSection) {
    nextSection.scrollIntoView({ behavior: "smooth" });
  }
};
</script>
