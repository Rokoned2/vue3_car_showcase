<template>
  <div class="w-fit">
    <Listbox
      v-model="selected"
      :model-value="selected"
      @update:model-value="handleUpdateParams"
    >
      <div class="relative w-fit z-10">
        <ListboxButton class="custom-filter__btn">
          <span class="block truncate">{{ selected.title }}</span>
          <img
            :src="chevronUpDown"
            width="20"
            height="20"
            class="ml-4 object-contain"
            alt="chevron_up-down"
          />
        </ListboxButton>
        <transition
          leave-active-class="transition duration-100 ease-in"
          leave-from-class="opacity-100"
          leave-to-class="opacity-0"
        >
          <ListboxOptions class="custom-filter__options">
            <ListboxOption
              v-slot="{ active, selected }"
              v-for="option in options"
              :key="option.title"
              :value="option"
              as="template"
            >
              <li
                :class="[
                  active ? 'bg-primary-blue text-white' : 'text-gray-900',
                  'relative cursor-default select-none py-2 pl-10 pr-4',
                ]"
              >
                <span
                  :class="selected ? 'font-medium' : 'font-normal'"
                  class="block truncate"
                >
                  {{ option.title }}
                </span>
              </li>
            </ListboxOption>
          </ListboxOptions>
        </transition>
      </div>
    </Listbox>
  </div>
</template>

<script setup>
import {
  Listbox,
  ListboxButton,
  ListboxOptions,
  ListboxOption,
} from "@headlessui/vue";

import { updateSearchParams } from "../utils";
import { useRouter } from "vue-router";

const props = defineProps(["title", "options"]);
const router = useRouter();

const selected = props.options[0];

const chevronUpDown =
  import.meta.env.BASE_URL + "src/assets/chevron-up-down.svg";

const handleUpdateParams = (e) => {
  const newPathName = updateSearchParams(props.title, e.value.toLowerCase());

  router.push(newPathName);
};
</script>
