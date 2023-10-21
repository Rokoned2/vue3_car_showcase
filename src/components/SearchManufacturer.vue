<template>
  <div class="search-manufacturer">
    <Combobox
      v-model="selected"
      :model-value="selected"
      @update:model-value="$emit('newManufacturer', selected)"
    >
      <div class="relative w-full">
        <ComboboxButton class="absolute top-[14px]">
          <img
            :src="carLogo"
            class="ml-4"
            width="20"
            height="20"
            aria-hidden="true"
            alt="car logo"
          />
        </ComboboxButton>
        <ComboboxInput
          class="search-manufacturer__input"
          :displayValue="(item) => item"
          @change="query = $event.target.value"
          placeholder="Volkswagen..."
        />
        <TransitionRoot
          leave="transition ease-in duration-100"
          leaveFrom="opacity-100"
          leaveTo="opacity-0"
          @after-leave="query = ''"
        >
          <ComboboxOptions
            class="absolute mt-1 max-h-60 w-full overflow-auto rounded-md bg-white py-1 text-base shadow-lg ring-1 ring-black ring-opacity-5 focus:outline-none sm:text-sm"
          >
            <ComboboxOption
              v-if="filteredManufacturers.length === 0 && query !== ''"
              :value="query"
              class="search-manufacturer__option"
            >
              Create "{{ query }}"
            </ComboboxOption>

            <ComboboxOption
              as="template"
              v-for="item in filteredManufacturers"
              :key="item"
              :value="item"
              v-slot="{ selected, active }"
            >
              <li
                class="relative search-manufacturer__option"
                :class="{
                  'bg-primary-blue text-white': active,
                  'text-gray-900': !active,
                }"
              >
                <span
                  class="block truncate"
                  :class="{ 'font-medium': selected, 'font-normal': !selected }"
                >
                  {{ item }}
                </span>
                <span
                  v-if="selected"
                  class="absolute inset-y-0 left-0 flex items-center pl-3"
                  :class="{
                    'text-white': active,
                    'text-pribg-primary-purple': !active,
                  }"
                >
                </span>
              </li>
            </ComboboxOption>
          </ComboboxOptions>
        </TransitionRoot>
      </div>
    </Combobox>
  </div>
</template>

<script setup>
import { computed, ref } from "vue";
import {
  Combobox,
  ComboboxInput,
  ComboboxButton,
  ComboboxOptions,
  ComboboxOption,
  TransitionRoot,
} from "@headlessui/vue";
import { manufacturers } from "../constants";

const emit = defineEmits(["newManufacturer"]);
const props = defineProps(["manufacturer"]);

const query = ref("");
const carLogo = import.meta.env.BASE_URL + "src/assets/car-logo.svg";
const selected = props.manufacturer;

const filteredManufacturers = computed(() => {
  return query.value === ""
    ? manufacturers
    : manufacturers.filter((item) =>
        item
          .toLowerCase()
          .replace(/\s+/g, "")
          .includes(query.value.toLowerCase().replace(/\s+/g, ""))
      );
});
</script>
