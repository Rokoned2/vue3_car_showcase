<template>
  <TransitionRoot appear :show="isOpen" as="template">
    <Dialog as="div" class="relative z-10">
      <TransitionChild
        as="template"
        enter="duration-300 ease-out"
        enter-from="opacity-0"
        enter-to="opacity-100"
        leave="duration-200 ease-in"
        leave-from="opacity-100"
        leave-to="opacity-0"
      >
        <div class="fixed inset-0 bg-black bg-opacity-25" />
      </TransitionChild>

      <div class="fixed inset-0 overflow-y-auto">
        <div
          class="flex min-h-full items-center justify-center p-4 text-center"
        >
          <TransitionChild
            as="template"
            enter="duration-300 ease-out"
            enter-from="opacity-0 scale-95"
            enter-to="opacity-100 scale-100"
            leave="duration-200 ease-in"
            leave-from="opacity-100 scale-100"
            leave-to="opacity-0 scale-95"
          >
            <DialogPanel
              class="relative w-full max-w-lg max-h-[90vh] overflow-y-auto transform rounded-2xl bg-white p-6 text-left shadow-xl transition-all flex flex-col gap-5"
            >
              <button
                type="button"
                class="absolute top-2 right-2 z-10 w-fit p-2 bg-primary-blue-100 rounded-full"
                @click="$emit('close')"
              >
                <img
                  :src="closeIcon"
                  alt="close"
                  width="20"
                  height="20"
                  class="object-contain"
                />
              </button>

              <div class="flex-1 flex flex-col gap-3">
                <div
                  class="relative w-full h-40 bg-pattern bg-cover bg-center rounded-lg"
                >
                  <img
                    :src="generateCarImageUrl(car)"
                    alt="car model"
                    class="object-contain fill"
                  />
                </div>

                <div class="flex gap-3">
                  <div
                    class="flex-1 relative w-full h-24 bg-primary-blue-100 rounded-lg"
                  >
                    <img
                      :src="generateCarImageUrl(car, '29')"
                      alt="car model"
                      class="object-contain fill"
                    />
                  </div>
                  <div
                    class="flex-1 relative w-full h-24 bg-primary-blue-100 rounded-lg"
                  >
                    <img
                      :src="generateCarImageUrl(car, '33')"
                      alt="car model"
                      class="object-contain fill"
                    />
                  </div>
                  <div
                    class="flex-1 relative w-full h-24 bg-primary-blue-100 rounded-lg"
                  >
                    <img
                      :src="generateCarImageUrl(car, '13')"
                      alt="car model"
                      class="object-contain fill"
                    />
                  </div>
                </div>
              </div>

              <div class="flex-1 flex flex-col gap-2">
                <h2 class="font-semibold text-xl capitalize">
                  {{ car.make }} {{ car.model }}
                </h2>

                <div class="mt-3 flex flex-wrap gap-4">
                  <div
                    v-for="(carValue, carKey) in car"
                    :key="carKey"
                    class="flex justify-between gap-5 w-full text-right"
                  >
                    <h4 class="text-grey capitalize">
                      {{ carKey.split("_").join(" ") }}
                    </h4>
                    <p class="text-black-100 font-semibold">
                      {{ carValue }}
                    </p>
                  </div>
                </div>
              </div>
            </DialogPanel>
          </TransitionChild>
        </div>
      </div>
    </Dialog>
  </TransitionRoot>
</template>

<script setup>
import {
  TransitionRoot,
  TransitionChild,
  Dialog,
  DialogPanel,
} from "@headlessui/vue";
import { generateCarImageUrl } from "../utils";

const props = defineProps(["car", "isOpen"]);

const emit = defineEmits(["close"]);

const closeIcon = import.meta.env.BASE_URL + "src/assets/close.svg";
</script>
