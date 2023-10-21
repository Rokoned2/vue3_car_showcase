<template>
  <form class="searchbar" @submit.prevent="handleSearch">
    <div class="searchbar__item">
      <SearchManufacturer
        :manufacturer="manufacturer"
        @newManufacturer="updateManufacturer"
      />
      <SearchButton otherClasses="sm:hidden" />
    </div>
    <div class="searchbar__item">
      <img
        :src="modelIcon"
        width="25"
        height="25"
        class="absolute w-[20px] h-[20px] ml-4"
        alt="car model"
      />
      <input
        type="text"
        id="model"
        v-model="model"
        placeholder="Tiguan..."
        className="searchbar__input"
      />
      <SearchButton otherClasses="sm:hidden" />
    </div>
    <SearchButton otherClasses="max-sm:hidden" />
  </form>
</template>

<script setup>
import { ref } from "vue";
import { useRouter } from "vue-router";
import SearchManufacturer from "./SearchManufacturer.vue";
import SearchButton from "./SearchButton.vue";

const router = useRouter();

const modelIcon = import.meta.env.BASE_URL + "src/assets/model-icon.png";
const manufacturer = ref("");
const model = ref("");

const updateManufacturer = (newManufacturer) => {
  manufacturer.value = newManufacturer;
};

const handleSearch = () => {
  if (manufacturer.value.trim() === "" && model.value.trim() === "") {
    return alert("Please provide some input");
  }

  updateSearchParams(
    model.value.toLowerCase(),
    manufacturer.value.toLowerCase()
  );
};

const updateSearchParams = (model, manufacturer) => {
  // Create a new URLSearchParams object using the current URL search parameters
  const searchParams = new URLSearchParams(window.location.search);

  // Update or delete the 'model' search parameter based on the 'model' value
  if (model) {
    searchParams.set("model", model);
  } else {
    searchParams.delete("model");
  }

  // Update or delete the 'manufacturer' search parameter based on the 'manufacturer' value
  if (manufacturer) {
    searchParams.set("manufacturer", manufacturer);
  } else {
    searchParams.delete("manufacturer");
  }

  // Generate the new pathname with the updated search parameters
  const newPathname = `${window.location.pathname}?${searchParams.toString()}`;

  router.push(newPathname);
};
</script>
