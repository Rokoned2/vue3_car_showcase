<template>
  <main class="overflow-hidden">
    <Hero />

    <div class="mt-12 padding-x padding-y max-width" id="discover">
      <div class="home__text-container">
        <h1 class="text-4xl font-extrabold">Car Catalogue</h1>
        <p>Explore out cars you might like</p>
      </div>

      <div class="home__filters">
        <SearchBar />

        <div class="home__filter-container">
          <CustomFilter title="fuel" :options="fuels" />
          <CustomFilter title="year" :options="yearsOfProduction" />
        </div>
      </div>

      <section v-if="!isDataEmpty">
        <div class="home__cars-wrapper">
          <CarCard v-for="car in allCars" :car="car" :key="car.model" />
        </div>

        <ShowMore :pageNumber="pageNumber" :isNext="isNext" />
      </section>

      <div v-else class="home__error-container">
        <h2 class="text-black text-xl font-bold">Oops, no results</h2>
        <!-- <p>{{ allCars.message }}</p> -->
      </div>
    </div>
  </main>
</template>

<script setup>
import { ref, watch, computed } from "vue";
import { useRoute } from "vue-router";
import Hero from "../components/Hero.vue";
import CarCard from "../components/CarCard.vue";
import SearchBar from "../components/SearchBar.vue";
import ShowMore from "../components/ShowMore.vue";
import CustomFilter from "../components/CustomFilter.vue";

import { fetchCars } from "../utils";
import { fuels, yearsOfProduction } from "../constants";

const route = useRoute();

const allCars = ref([]);
const isDataEmpty = ref(true);
const searchParams = ref(route.query);

const pageNumber = computed(() => {
  return (searchParams.value.limit || 10) / 10;
});

const isNext = computed(() => {
  return (searchParams.value.limit || 10) > allCars.value.length;
});

const getCars = async () => {
  allCars.value = await fetchCars({
    manufacturer: searchParams.value.manufacturer || "",
    year: searchParams.value.year || 2022,
    fuel: searchParams.value.fuel || "",
    limit: searchParams.value.limit || 10,
    model: searchParams.value.model || "",
  });
  isDataEmpty.value =
    !Array.isArray(allCars.value) || allCars.value.length < 1 || !allCars.value;
};

getCars();

watch(route, () => {
  searchParams.value = route.query;
  getCars();
});
</script>
