<template>
  <footer
    className="flex flex-col text-black-100  mt-5 border-t border-gray-100"
  >
    <div
      className="flex max-md:flex-col flex-wrap justify-between gap-5 sm:px-16 px-6 py-10"
    >
      <div className="flex flex-col justify-start items-start gap-6">
        <img
          :src="logoImage"
          alt="logo"
          width="118"
          height="18"
          className="object-contain"
        />
        <p className="text-base text-gray-700">
          Carhub 2023 <br />
          All Rights Reserved &copy;
        </p>
      </div>

      <div className="footer__links">
        <div
          v-for="item in footerLinks"
          :key="item.title"
          className="footer__link"
        >
          <h3 className="font-bold">{{ item.title }}</h3>
          <div className="flex flex-col gap-5">
            <router-link
              v-for="link in item.links"
              :key="link.title"
              :to="link.url"
              class="text-gray-500"
            >
              {{ link.title }}
            </router-link>
          </div>
        </div>
      </div>
    </div>

    <div
      className="flex justify-between items-center flex-wrap mt-10 border-t border-gray-100 sm:px-16 px-6 py-10"
    >
      <p>@2023 CarHub. All rights reserved</p>

      <div className="footer__copyrights-link">
        <div className="text-gray-500">Privacy & Policy</div>
        <div className="text-gray-500">Terms & Condition</div>
      </div>
    </div>
  </footer>
</template>

<script setup>
import { footerLinks } from "../constants";

const logoImage = import.meta.env.BASE_URL + "src/assets/logo.svg";
</script>

<style scoped></style>
