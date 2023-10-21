<template>
  <header className="w-full absolute z-10">
    <nav
      className="max-w-[1440px] mx-auto flex justify-between items-center sm:px-16 px-6 py-4 bg-transparent"
    >
      <router-link to="/" className="flex justify-center items-center">
        <img
          :src="logoImage"
          alt="logo"
          width="118"
          height="18"
          className="object-contain"
        />
      </router-link>

      <CustomButton
        title="Sign in"
        containerStyles="text-primary-blue rounded-full bg-white min-w-[130px]"
      />
    </nav>
  </header>
</template>

<script setup>
import CustomButton from "./CustomButton.vue";

const logoImage = import.meta.env.BASE_URL + "src/assets/logo.svg";
</script>
