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
                  {{ artist.artist_name }}
                </DialogTitle>
              </div>
              <div class="mt-6 flex">
                <div class="mr-6">
                  <img :src="artist.avatar" alt="Artist Avatar" class="w-40 h-auto border-4 border-gray-400 rounded-full" />
                </div>
                <div class="text-sm text-gray-500">
                  <ul class="space-y-2">
                    <li><strong>Date of Birth:</strong> {{ artist.birth_date }}</li>
                    <li><strong>Country:</strong> {{ artist.country }}</li>
                    <li><strong>Biography:</strong> {{ artist.bio }}</li>
                    <li><strong>Sort Order:</strong> {{ artist.sort_order }}</li>
                    <li><strong>Status:</strong> {{ artist.status ? 'Active' : 'Inactive' }}</li>
                  </ul>
                </div>
              </div>
              <div class="mt-6">
                <h2 class="text-lg font-semibold text-grey-800">Albums</h2>
                <div class="mt-4 space-y-4">
                  <div v-for="album in artist.albums" :key="album.id" class="flex items-center">
                    <img :src="album.album_image" alt="Album" class="w-16 h-16 object-cover rounded-md mr-4 border-4 border-gray-400" />
                    <div>
                      <div>{{ album.album_name }}</div>
                      <div class="text-sm text-gray-500">{{ album.album_year }}</div>
                    </div>
                  </div>
                </div>
              </div>
              <div class="mt-5 sm:mt-6">
                <RouterLink
                    type="button"
                    class="block rounded-md bg-green-800 px-3 py-2 text-center text-sm font-semibold text-white shadow-sm
                    hover:bg-white hover:text-green-800 hover:border-green-800 border-2 border-green-800 focus-visible:outline
                    focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-green-800"
                    to="/admin/artist"
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

const artist =
    {
      artist_name : "Olivia Fontaine",
      avatar : "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Artist-Images/Olivia-Fontaine.jpg",
      birth_date : "1984-12-12",
      country : "USA",
      bio : "Olivia Fontaine biography",
      songs : [1,2,3],
      albums: [
        {
          id: 1,
          album_name: "Echoes of Eternity",
          album_year: 2020,
          album_image: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Album-Images/Echoes-of-Eternity.jpg"
        },
        {
          id: 6,
          album_name: "Rhythm of the Cosmos",
          album_year: 2022,
          album_image: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Album-Images/Rhythm-of-the-Cosmos.jpg"
        }
      ],
      sort_order : 0,
      status : true
    }
</script>
