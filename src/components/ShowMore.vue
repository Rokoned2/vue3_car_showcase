<template>
  <div className="w-full flex-center gap-5 mt-10">
    <CustomButton
      v-show="!isNext"
      btnType="button"
      title="Show More"
      containerStyles="bg-primary-blue rounded-full text-white"
      @handleClick="handleNavigation"
    />
  </div>
</template>

<script setup>
import { useRouter } from "vue-router";
import CustomButton from "./CustomButton.vue";
import { updateSearchParams } from "../utils";

const props = defineProps(["isNext", "pageNumber"]);

const router = useRouter();

const handleNavigation = () => {
  // Calculate the new limit based on the page number and navigation type
  const newLimit = (props.pageNumber + 1) * 10;

  // Update the "limit" search parameter in the URL with the new value
  const newPathname = updateSearchParams("limit", `${newLimit}`);

  router.push(newPathname);
};
</script>
