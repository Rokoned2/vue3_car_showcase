<template>
  <div className="car-card group">
    <div className="car-card__content">
      <h2 className="car-card__content-title">{{ make }} {{ model }}</h2>
    </div>

    <p className="flex mt-6 text-[32px] leading-[38px] font-extrabold">
      <span className="self-start text-[14px] leading-[17px] font-semibold"
        >$</span
      >
      {{ carRent }}
      <span className="self-end text-[14px] leading-[17px] font-medium"
        >/day</span
      >
    </p>

    <div className="relative w-full h-40 my-3 object-contain">
      <img :src="carImageUrl" alt="car model" className="fill object-contain" />
    </div>

    <div className="relative flex w-full mt-2">
      <div
        className="flex group-hover:invisible w-full justify-between text-grey"
      >
        <div className="flex flex-col justify-center items-center gap-2">
          <img
            :src="steeringWheel"
            width="20"
            height="20"
            alt="steering wheel"
          />
          <p className="text-[14px] leading-[17px]">
            {{ transmission === "a" ? "Automatic" : "Manual" }}
          </p>
        </div>
        <div className="car-card__icon">
          <img :src="tire" width="20" height="20" alt="seat" />
          <p className="car-card__icon-text">{{ drive.toUpperCase() }}</p>
        </div>
        <div className="car-card__icon">
          <img :src="gas" width="20" height="20" alt="seat" />
          <p className="car-card__icon-text">{{ city_mpg }} MPG</p>
        </div>
      </div>

      <div className="car-card__btn-container">
        <CustomButton
          title="View More"
          containerStyles="w-full py-[16px]
        rounded-full bg-primary-blue"
          textStyles="text-white text-[14px]
        leading-[17px] font-bold"
          :rightIcon="rightArrow"
          @handleClick="isOpen = true"
        />
      </div>
    </div>

    <CarDetails :isOpen="isOpen" @close="isOpen = false" :car="car" />
  </div>
</template>

<script setup>
import { ref, computed } from "vue";
import { calculateCarRent, generateCarImageUrl } from "../utils";
import CarDetails from "./CarDetails.vue";
import CustomButton from "./CustomButton.vue";

const props = defineProps(["car"]);

const { city_mpg, year, make, model, transmission, drive } = props.car;

const isOpen = ref(false);

const steeringWheel =
  import.meta.env.BASE_URL + "src/assets/steering-wheel.svg";
const rightArrow = import.meta.env.BASE_URL + "src/assets/right-arrow.svg";
const tire = import.meta.env.BASE_URL + "src/assets/tire.svg";
const gas = import.meta.env.BASE_URL + "src/assets/gas.svg";

const carImageUrl = computed(() => {
  return generateCarImageUrl(props.car);
});

const carRent = computed(() => {
  return calculateCarRent(city_mpg, year);
});
</script>
