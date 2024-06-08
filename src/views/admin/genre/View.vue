<template>
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
        <div class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity" />
      </TransitionChild>

      <div class="fixed inset-0 z-10 w-screen overflow-y-auto">
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
                class="relative transform overflow-hidden rounded-lg bg-white px-4 pb-4 pt-5 text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg sm:p-6"
            >
              <div class="bg-gray-100 px-4 py-5 sm:px-6">
                <DialogTitle as="h1" class="text-center text-2xl font-semibold leading-6 text-green-800">
                  {{ genre.genre_name }}
                </DialogTitle>
              </div>
              <div class="mt-6">
                <div class="text-sm text-gray-500">
                  <ul class="space-y-2">
                    <li class="flex justify-center">
                      <img :src="genre.genre_image" alt="Genre Image" class="max-w-full h-auto border-4 border-gray-500 rounded-lg" style="max-width: 250px; height: auto;" />
                    </li>

                    <li><strong>Sort Order:</strong> {{ genre.sort_order }}</li>
                    <li><strong>Status:</strong> {{ genre.status }}</li>
                  </ul>
                </div>
              </div>
              <div class="mt-5 sm:mt-6">
                <RouterLink
                    type="button"
                    class="block rounded-md bg-green-800 px-3 py-2 text-center text-sm font-semibold text-white shadow-sm
                    hover:bg-white hover:text-green-800 hover:border-green-800 border-2 border-green-800 focus-visible:outline
                    focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-green-800"
                    to="/admin/genre"
                    ref="cancelButtonRef">
                  Close
                </RouterLink>
              </div>
            </DialogPanel>
          </TransitionChild>
        </div>
      </div>
    </Dialog>
  </TransitionRoot>
</template>

<script setup>
import { ref } from 'vue'
import { Dialog, DialogPanel, DialogTitle, TransitionChild, TransitionRoot } from '@headlessui/vue'

const open = ref(true)

const genre =
    {
      id: 1,
      genre_name: "Pop",
      genre_description: "The description of Pop",
      genre_image : "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Genre-Images/Pop.jpg",
      sort_order: 0,
      status: true
    }
</script>
