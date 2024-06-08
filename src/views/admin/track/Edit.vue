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
              <form v-on:submit.prevent="saveTrack">
                <div>
                  <div class="mt-3 sm:mt-5">
                    <DialogTitle as="h1" class="text-center text-2xl font-semibold leading-6 text-green-800">
                      {{ track.track_name }}
                    </DialogTitle>
                    <div class="mt-4">
                      <div class="grid max-w-2xl grid-cols-1 gap-x-6 gap-y-4 sm:grid-cols-6">
                        <div class="sm:col-span-8">
                          <label
                              for="track_name"
                              class="block text-sm font-medium leading-6 text-gray-900">
                            Name of the Track
                          </label>
                          <div class="mt-2">
                            <div
                                class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2
                                focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <input
                                  type="text"
                                  name="track_name"
                                  id="track_name"
                                  class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                  v-model="track.track_name"/>
                            </div>
                          </div>
                        </div>

                        <!-------------------------------- File ---------------------------------->

                        <div class="sm:col-span-8">
                          <label
                              for="file"
                              class="block text-sm font-medium leading-6 text-gray-900">
                            Track File
                          </label>
                          <div class="mt-2">
                            <div
                                class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2
                                focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <input
                                  type="file"
                                  name="file"
                                  id="file"
                                  class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900
                                  placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"/>
                            </div>
                          </div>
                        </div>

                        <!-------------------------------- File Image---------------------------------->

                        <div class="sm:col-span-8">
                          <label
                              for="file"
                              class="block text-sm font-medium leading-6 text-gray-900">
                            Track Image
                          </label>
                          <div class="mt-2">
                            <div
                                class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2
                                focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <input
                                  type="file"
                                  name="file"
                                  id="file"
                                  class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900
                                  placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"/>
                            </div>
                          </div>
                        </div>

                        <!--------------------------------- Genre -------------------------------->

                        <div class="sm:col-span-4">
                          <label for="genre" class="block text-sm font-medium leading-6 text-gray-900">
                            Genre
                          </label>
                          <div class="mt-2">
                            <div class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <select
                                  v-model="track.genre.genre_name"
                                  name="genre"
                                  id="genre"
                                  class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900
                                  placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6">
                                <option value="Pop">Pop</option>
                                <option value="Electronic">Electronic</option>
                                <option value="Blues">Blues</option>
                                <option value="Techno">Techno</option>
                                <option value="House">House</option>
                              </select>
                            </div>
                          </div>
                        </div>

                        <!---------------------------------  Duration -------------------------------->

                        <div class="sm:col-span-3">
                          <label for="track_duration" class="block text-sm font-medium leading-6 text-gray-900">
                            Duration in Seconds
                          </label>
                          <div class="mt-2">
                            <div class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2
                            focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <select
                                  v-model="track.track_duration"
                                  name="track_duration"
                                  id="track_duration"
                                  class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900
                                  placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6">
                                <option value="170">170</option>
                                <option value="171">171</option>
                                <option value="172">172</option>
                                <option value="173">173</option>
                                <option value="174">174</option>
                                <option value="175">175</option>
                                <option value="176">176</option>
                                <option value="177">177</option>
                                <option value="178">178</option>
                                <option value="179">179</option>
                                <option value="180">180</option>
                                <option value="181">181</option>
                                <option value="182">182</option>
                                <option value="183">183</option>
                                <option value="184">184</option>
                                <option value="185">185</option>
                                <option value="186">186</option>
                                <option value="187">187</option>
                                <option value="188">188</option>
                                <option value="189">189</option>
                                <option value="190">190</option>
                              </select>
                            </div>
                          </div>
                        </div>

                        <!---------------------------------  Artist -------------------------------->

                        <div class="sm:col-span-4">
                          <label for="artist" class="block text-sm font-medium leading-6 text-gray-900">
                            Artist
                          </label>
                          <div class="mt-2">
                            <div class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <select
                                  v-model="track.artist.artist_name"
                                  name="artist"
                                  id="artist"
                                  class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900
                                  placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6">
                                <option value="Olivia Fontaine">Olivia Fontaine</option>
                                <option value="Sophia Beaumont">Sophia Beaumont</option>
                                <option value="William Montgomery">William Montgomery</option>
                                <option value="Benjamin Sterling">Benjamin Sterling</option>
                                <option value="Liam Sinclair">Liam Sinclair</option>
                              </select>
                            </div>
                          </div>
                        </div>

                        <!---------------------------------  Album -------------------------------->

                        <div class="sm:col-span-4">
                          <label
                              for="album"
                              class="block text-sm font-medium leading-6 text-gray-900">
                            Album
                          </label>
                          <div class="mt-2">
                            <div class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <input
                                  type="text"
                                  name="album"
                                  id="album"
                                  class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400
                                  focus:ring-0 sm:text-sm sm:leading-6"
                                  v-model="track.album.album_name"/>
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
                      to="/admin/track"
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

const track = ref({
      id: 1,
      track_name: "You are Enchanted",
      file: "FILE_PATH",
      genre: { id: 1, genre_name: "Pop" },
      track_duration: 187,
      artist: { id: 1, artist_name : 'Olivia Fontaine' },
      album: { id: 1, album_name: "Echoes of Eternity" },
      sort_order: 0,
      status: true
    }
)
const saveTrack = () => {
  console.log(track)

  // route the user to the track list page
  router.push('/admin/track')
}
</script>
