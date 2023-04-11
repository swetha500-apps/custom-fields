<template>
  <div>
    <input ref="fileInput" type="file" @change="handleFileInputChange" />
    <div v-if="file" class="filename">
      <button @click="open = true">{{ file.name }}</button>
    </div>

    <div v-if="open">
      <TransitionRoot as="template" :show="open">
        <Dialog as="div" class="relative z-10" @close="open = false">
          <TransitionChild
            as="template"
            enter="ease-out duration-300"
            enter-from="opacity-0"
            enter-to="opacity-100"
            leave="ease-in duration-200"
            leave-from="opacity-100"
            leave-to="opacity-0"
          >
            <div
              class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity"
            />
          </TransitionChild>

          <div class="fixed inset-0 z-10 overflow-y-auto">
            <div
              class="flex min-h-full items-end justify-center p-4 text-center sm:items-center sm:p-0"
            >
              <TransitionChild
                as="template"
                enter="ease-out duration-300"
                enter-from="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
                enter-to="opacity-100 translate-y-0 sm:scale-100"
                leave="ease-in duration-200"
                leave-from="opacity-100 translate-y-0 sm:scale-100"
                leave-to="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
              >
                <DialogPanel
                  class="relative transform overflow-hidden rounded-lg bg-white px-4 pb-4 pt-5 text-left shadow-xl transition-all sm:my-8 h-[90vh] w-[1700px] sm:p-6"
                >
                  <div class="absolute right-0 top-0 hidden pr-4 pt-4 sm:block">
                    <button
                      type="button"
                      class="rounded-md bg-white text-gray-400 hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2"
                      @click="open = false"
                    >
                      <span class="sr-only">Close</span>
                      <XMarkIcon class="h-6 w-6" aria-hidden="true" />
                    </button>
                  </div>
                  <div>
                    <div class="mt-3 text-center sm:ml-4 sm:mt-0 sm:text-left">
                      <DialogTitle
                        as="h3"
                        class="text-base font-semibold leading-6 text-gray-900"
                      >
                        {{ file.name }}</DialogTitle
                      >
                      <div class="mt-2">
                        <div>
                          <embed
                            :src="fileUrl"
                            type="application/pdf"
                            width="100%"
                            class="h-[78vh]"
                          />
                        </div>
                      </div>
                    </div>
                  </div>
                </DialogPanel>
              </TransitionChild>
            </div>
          </div>
        </Dialog>
      </TransitionRoot>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref, computed } from "vue";
import {
  Dialog,
  DialogPanel,
  DialogTitle,
  TransitionChild,
  TransitionRoot,
} from "@headlessui/vue";
import { ExclamationTriangleIcon, XMarkIcon } from "@heroicons/vue/24/outline";
const open = ref(false);
const file = ref<File | null>(null);
// Compute the URL for the selected file
const fileUrl = computed(() => {
  return file.value ? URL.createObjectURL(file.value) : "";
});
// Handle changes to the file input element and set the value of the file ref
const handleFileInputChange = () => {
  const input = document.querySelector(
    'input[type="file"]'
  ) as HTMLInputElement;
  if (input.files && input.files[0]) {
    file.value = input.files[0];
  }
};
</script>

<style scoped></style>
