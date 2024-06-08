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
        <div class="flex min-h-full items-end justify-center p-4 text-center sm:items-center sm:p-0">
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
                  {{ track.track_name }}
                </DialogTitle>
              </div>

              <div class="mt-6">
                <div class="text-sm text-gray-500">
                  <ul class="space-y-2">
                    <li class="flex justify-center items-center relative w-40 h-40 mx-auto">
                      <img
                          :src="track.track_image"
                          alt="Track"
                          :class="{ 'border-green-500': isPlaying }"
                          class="w-full h-full object-cover rounded-full border-4 border-gray-400"
                      />
                      <div class="absolute inset-0 flex items-center justify-center">
                        <svg
                            v-if="!isPlaying"
                            @click="togglePlay"
                            @mouseenter="hovering = true"
                            @mouseleave="hovering = false"
                            :class="{ 'border-green-500': hovering }"
                            class="w-12 h-12 text-white fill-current cursor-pointer"
                            xmlns="http://www.w3.org/2000/svg"
                            viewBox="0 0 24 24"
                        >
                          <path d="M8 5v14l11-7z" />
                        </svg>
                        <svg
                            v-else
                            @click="togglePlay"
                            @mouseenter="hovering = true"
                            @mouseleave="hovering = false"
                            :class="{ 'border-green-500': hovering }"
                            class="w-12 h-12 text-white fill-current cursor-pointer"
                            xmlns="http://www.w3.org/2000/svg"
                            viewBox="0 0 24 24"
                        >
                          <path d="M6 19h4V5H6v14zm8-14v14h4V5h-4z" />
                        </svg>
                      </div>
                      <audio ref="audio" :src="track.file" @timeupdate="updateProgress" @loadedmetadata="setDuration" @ended="handleEnded"></audio>
                    </li>

                    <li>
                      <div class="relative pt-1 mb-4">
                        <div class="flex mb-2 items-center justify-between">
                          <div>
        <span class="text-xs font-semibold inline-block py-1 px-2 uppercase rounded-full text-green-800 bg-green-200">
          {{ formatTime(currentTime) }}
        </span>
                          </div>
                          <div class="text-right">
        <span class="text-xs font-semibold inline-block text-green-800">
          {{ formatTime(duration) }}
        </span>
                          </div>
                        </div>
                        <div class="h-2 relative max-w-full rounded-full overflow-hidden">
                          <div class="w-full h-full bg-gray-200 absolute"></div>
                          <div class="h-full bg-green-800 absolute" :style="{ width: `${progress}%` }"></div>
                          <input
                              type="range"
                              min="0"
                              :max="duration"
                              v-model="currentTime"
                              @input="seekAudio"
                              class="absolute w-full h-full opacity-0 cursor-pointer"
                          />
                        </div>
                      </div>
                    </li>

                    <div class="px-4 py-2"> <!-- Add padding to the container -->
                      <li class="my-4">
                        <div class="flex justify-around">
                          <div class="flex flex-col items-center mr-4">
                            <h3 class="text-center font-semibold">Artist</h3>
                            <img :src="track.artist.avatar" alt="Artist Image" class="w-24 h-24 object-cover mt-2 rounded-lg border-4 border-gray-500" />
                            <p class="text-center mt-2">{{ track.artist.artist_name }}</p>
                          </div>
                          <div class="flex flex-col items-center mr-4">
                            <h3 class="text-center font-semibold">Album</h3>
                            <img :src="track.album.album_image" alt="Album Image" class="w-24 h-24 object-cover mt-2 rounded-lg border-4 border-gray-500" />
                            <p class="text-center mt-2">{{ track.album.album_name }}</p>
                          </div>
                          <div class="flex flex-col items-center">
                            <h3 class="text-center font-semibold">Genre</h3>
                            <img :src="track.genre.genre_image" alt="Genre Image" class="w-24 h-24 object-cover mt-2 rounded-lg border-4 border-gray-500" />
                            <p class="text-center mt-2">{{ track.genre.genre_name }}</p>
                          </div>
                        </div>
                      </li>
                    </div>


                    <li class="mt-4">
                      <strong>Duration:</strong> {{ track.track_duration }} seconds
                    </li>

                    <li><strong>Sort Order:</strong> {{ track.sort_order }}</li>
                    <li><strong>Status:</strong> {{ track.status ? 'Active' : 'Inactive' }}</li>
                  </ul>
                </div>
              </div>
              <div class="mt-5 sm:mt-6">
                <RouterLink
                    type="button"
                    class="block rounded-md bg-green-800 px-3 py-2 text-center text-sm font-semibold text-white shadow-sm hover:bg-white hover:text-green-800 hover:border-green-800 border-2 border-green-800 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-green-800"
                    to="/admin/track"
                    ref="cancelButtonRef"
                >
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
const isPlaying = ref(false)
const hovering = ref(false)
const audio = ref(null)
const currentTime = ref(0)
const duration = ref(0)

const track = {
  id: 1,
  track_name: "You are Enchanted",
  track_image: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track1.jpg",
  file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track1.mp3",
  genre: {
    id: 1,
    genre_name: "Pop",
    genre_image: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Genre-Images/Pop.jpg"
  },
  track_duration: 164,
  artist: {
    id: 1,
    artist_name: 'Olivia Fontaine',
    avatar: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Artist-Images/Olivia-Fontaine.jpg",
  },
  album: {
    id: 1,
    album_name: "Echoes of Eternity",
    album_image: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Album-Images/Echoes-of-Eternity.jpg",
  },
  sort_order: 0,
  status: true
}

const togglePlay = () => {
  if (isPlaying.value) {
    audio.value.pause()
  } else {
    audio.value.play()
  }
  isPlaying.value = !isPlaying.value
}

const updateProgress = () => {
  currentTime.value = audio.value.currentTime
}

const setDuration = () => {
  duration.value = audio.value.duration
}

const seekAudio = () => {
  audio.value.currentTime = currentTime.value
}

const formatTime = (time) => {
  const minutes = Math.floor(time / 60)
  const seconds = Math.floor(time % 60).toString().padStart(2, '0')
  return `${minutes}:${seconds}`
}

const handleEnded = () => {
  isPlaying.value = false
}
</script>

<style scoped>
.container {
  display: flex;
  justify-content: space-around;
}
.column {
  text-align: center;
  width: 30%;
}
.column img {
  max-width: 100%;
  height: auto;
}
</style>
