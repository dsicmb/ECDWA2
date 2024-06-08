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
            class="flex min-h-full items-end justify-center p-4 text-center sm:items-center sm:p-0">
          <TransitionChild
              as="template"
              enter="ease-out duration-300"
              enter-from="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
              enter-to="opacity-100 translate-y-0 sm:scale-100"
              leave="ease-in duration-200"
              leave-from="opacity-100 translate-y-0 sm:scale-100"
              leave-to="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95">
            <DialogPanel
                class="relative transform overflow-hidden rounded-lg bg-white px-4 pb-4 pt-5 text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg sm:p-6">
              <div class="bg-gray-100 px-4 py-5 sm:px-6">
                <DialogTitle as="h1" class="text-center text-2xl font-semibold leading-6 text-green-800">
                  {{ album.album_name }}
                </DialogTitle>
              </div>
              <div class="mt-4 flex flex-col items-center mr-4">
                <img :src="album.album_image" alt="Album Image" class="border-4 border-gray-500 rounded-lg" style="width: 200px; border-radius: 15px;" />
                <div class="flex space-x-8 justify-center mt-4">
                  <div class="text-center">
                    <p class="font-bold">Artist</p>
                    <img :src="album.artist.avatar" alt="Artist Image" class="mx-auto border-4 border-gray-500 rounded-full" style="width: 120px; height: 120px;" />
                    <p class="mt-2">{{ album.artist.artist_name }}</p>
                  </div>
                  <div class="text-center mb-2">
                    <p class="font-bold">Genre</p>
                    <img :src="album.genre.genre_image" alt="Genre Image" class="mx-auto border-4 border-gray-500 rounded-full" style="width: 120px; height: 120px;" />
                    <p class="mt-2">{{ album.genre.genre_name }}</p>
                  </div>
                </div>
                <ul class="text-sm text-gray-500 mt-8 space-y-2">
                  <li><strong>Number of Tracks:</strong> {{ album.number_of_tracks }}</li>
                  <li><strong>Year:</strong> {{ album.album_year }}</li>
                  <li><strong>Description:</strong> {{ album.album_description }}</li>
                  <li><strong>Studio:</strong> {{ album.studio }}</li>
                  <li><strong>Producer:</strong> {{ album.producer }}</li>
                  <li><strong>Sort Order:</strong> {{ album.sort_order }}</li>
                  <li><strong>Status:</strong> {{ album.status }}</li>
                </ul>
              </div>
              <div class="mt-5 sm:mt-6">
                <RouterLink
                    type="button"
                    class="block rounded-md bg-green-800 px-3 py-2 text-center text-sm font-semibold text-white shadow-sm
                  hover:bg-white hover:text-green-800 hover:border-green-800 border-2 border-green-800 focus-visible:outline
                  focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-green-800"
                    to="/admin/album"
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

const album =
    {
      id: 1,
      album_name : "Echoes of Eternity",
      number_of_tracks : 10,
      album_year : 2020,
      album_description : "The description of Echoes of Eternity",
      album_image : "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Album-Images/Echoes-of-Eternity.jpg",
      artist : {
        id :1,
        artist_name : "Olivia Fontaine",
        avatar: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Artist-Images/Olivia-Fontaine.jpg",
        birth_date : "1984-12-12",
        country : "USA",
        bio : "Olivia Fontaine biography"
      },
      studio : "Echoes Songs",
      genre: {
        id: 1,
        genre_name: "Pop",
        genre_image: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Genre-Images/Pop.jpg"
      },
      producer : "Stevan Johns",
      sort_order : 0,
      status : true
    }
</script>







