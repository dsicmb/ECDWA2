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
              <form v-on:submit.prevent="saveAlbum">
                <div>
                  <div class="mt-3 sm:mt-5">
                    <DialogTitle as="h1" class="text-center text-2xl font-semibold leading-6 text-green-800">
                      {{ album.album_name }}
                    </DialogTitle>
                    <div class="mt-4">
                      <div class="grid max-w-2xl grid-cols-1 gap-x-6 gap-y-4 sm:grid-cols-6">
                        <div class="sm:col-span-8">
                          <label
                            for="album_name"
                            class="block text-sm font-medium leading-6 text-gray-900"
                          >
                            Album Name
                          </label>
                          <div class="mt-2">
                            <div
                              class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md"
                            >
                              <input
                                type="text"
                                name="album_name"
                                id="album_name"
                                class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                v-model="album.album_name"
                              />
                            </div>
                          </div>
                        </div>

                        <!------------------------ Number of Tracks -------------------------->

                        <div class="sm:col-span-4">
                          <label
                            for="number_of_tracks"
                            class="block text-sm font-medium leading-6 text-gray-900"
                          >
                            Number of Tracks
                          </label>
                          <div class="mt-2">
                            <div
                              class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md"
                            >
                              <input
                                type="text"
                                name="number_of_tracks"
                                id="number_of_tracks"
                                class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                v-model="album.number_of_tracks"
                              />
                            </div>
                          </div>
                        </div>

                        <!--------------------------------- Year -------------------------------->

                        <div class="sm:col-span-3">
                          <label
                            for="album_year"
                            class="block text-sm font-medium leading-6 text-gray-900"
                          >
                            Year
                          </label>
                          <div class="mt-2">
                            <div
                              class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md"
                            >
                              <input
                                type="text"
                                name="album_year"
                                id="album_year"
                                class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                v-model="album.album_year"
                              />
                            </div>
                          </div>
                        </div>

                        <!------------------------- Description --------------------------->

                        <div class="sm:col-span-8">
                          <label
                              for="album_description"
                              class="block text-sm font-medium leading-6 text-gray-900"
                          >
                            Description
                          </label>
                          <div class="mt-2">
                            <div
                                class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md"
                            >
                              <input
                                  type="text"
                                  name="album_description"
                                  id="album_description"
                                  class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                  v-model="album.album_description"
                              />
                            </div>
                          </div>
                        </div>

                        <!--------------------------- Album Image ----------------------------->

                        <div class="sm:col-span-8">
                          <label
                            for="album_image"
                            class="block text-sm font-medium leading-6 text-gray-900"
                          >
                            Album Image
                          </label>
                          <div class="mt-2">
                            <div
                              class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md"
                            >
                              <input
                                type="file"
                                name="album_image"
                                id="album_image"
                                class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                              />
                            </div>
                          </div>
                        </div>

                        <!------------------------------ Artist -------------------------------->

                        <div class="sm:col-span-3">
                          <label
                            for="artist"
                            class="block text-sm font-medium leading-6 text-gray-900"
                          >
                            Artist
                          </label>
                          <div class="mt-2">
                            <div
                              class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset
                              focus-within:ring-indigo-600 sm:max-w-md">
                              <select
                                v-model="album.artist.id"
                                name="artist"
                                id="artist"
                                class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400
                                focus:ring-0 sm:text-sm sm:leading-6">
                                <option value="1">Olivia Fontaine</option>
                                <option value="2">Sophia Beaumont</option>
                                <option value="3">William Montgomery</option>
                                <option value="3">Benjamin Sterling</option>
                                <option value="3">Liam Sinclair</option>
                              </select>
                            </div>
                          </div>
                        </div>

                        <!------------------------------ Studio -------------------------------->

                        <div class="sm:col-span-4">
                          <label
                            for="studio"
                            class="block text-sm font-medium leading-6 text-gray-900"
                          >
                            Studio
                          </label>
                          <div class="mt-2">
                            <div
                              class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md"
                            >
                              <input
                                type="text"
                                name="studio"
                                id="studio"
                                v-model="album.studio"
                                class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                              />
                            </div>
                          </div>
                        </div>

                        <!------------------------------ Genre -------------------------------->

                        <div class="sm:col-span-3">
                          <label
                            for="genre"
                            class="block text-sm font-medium leading-6 text-gray-900"
                          >
                            Genre
                          </label>
                          <div class="mt-2">
                            <div
                              class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md"
                            >
                              <input
                                type="text"
                                name="genre"
                                id="genre"
                                v-model="album.genre"
                                class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                              />
                            </div>
                          </div>
                        </div>

                        <!------------------------------ Producer -------------------------------->

                        <div class="sm:col-span-4 mb-8">
                          <label
                              for="producer"
                              class="block text-sm font-medium leading-6 text-gray-900"
                          >
                            Producer
                          </label>
                          <div class="mt-2">
                            <div
                                class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md"
                            >
                              <input
                                  type="text"
                                  name="producer"
                                  id="producer"
                                  v-model="album.producer"
                                  class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                              />
                            </div>
                          </div>
                        </div>
                      </div>


                    </div>
                  </div>
                </div>
                <div class="mt-5 sm:mt-6 flex gap-8">
                  <RouterLink
                      type="button"
                      class="inline-flex w-full justify-center rounded-md bg-green-800 px-3 py-2 text-sm font-semibold
                              text-white shadow-sm
                              hover:bg-white hover:text-green-800 hover:border-green-800 border-2 border-green-800
                              focus-visible:outline focus-visible:outline-2
                              focus-visible:outline-offset-2 focus-visible:outline-green-800 sm:col-start-2"
                      to="/admin/album"
                      ref="cancelButtonRef">
                    Back
                  </RouterLink>
                  <button
                      type="submit"
                      class="inline-flex w-full justify-center rounded-md bg-green-800 px-3 py-2 text-sm font-semibold
                              text-white shadow-sm hover:bg-white hover:text-green-800 hover:border-green-800 border-2
                              border-green-800 focus-visible:outline focus-visible:outline-2
                              focus-visible:outline-offset-2 focus-visible:outline-green-800 sm:col-start-2">
                    Save
                  </button>
                </div>
              </form>
            </DialogPanel>
          </TransitionChild>
        </div>
      </div>
    </Dialog>
  </TransitionRoot>
</template>

<script setup>
import { ref } from 'vue'
import { RouterLink } from 'vue-router';
import { Dialog, DialogPanel, DialogTitle, TransitionChild, TransitionRoot } from '@headlessui/vue'
import { useRouter } from 'vue-router'

const open = ref(true)

const router = useRouter()

const album = ref({
      id: 1,
      album_name : "Echoes of Eternity",
      number_of_tracks : 10,
      album_year : 2020,
      album_description : "The description of Echoes of Eternity",
      album_image : "IMAGE_URL",
      artist : {
        id :1,
        artist_name : "Olivia Fontaine",
        avatar : "IMAGE_URL",
        birth_date : "1984-12-12",
        country : "USA",
        bio : "Olivia Fontaine biography"
      },
      studio : "Echoes Songs",
      genre : "Pop",
      producer : "Stevan Johns",
      sort_order : 0,
      status : true
    }
)

const saveAlbum = () => {
  console.log(album)

  // route the user to the album list page
  router.push('/admin/album')
}
</script>
