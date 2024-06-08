<template>
  <div class="search-container">
    <span class="search-label">Search:</span>
    <input type="text" v-model="searchQuery" placeholder="What do you want to play?" class="search-input">
  </div>

  <div class="px-4 sm:px-6 lg:px-8">
    <div class="mt-8 flow-root">
      <div class="-mx-4 -my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
        <div class="inline-block min-w-full py-2 align-middle sm:px-6 lg:px-8">
          <table class="min-w-full divide-y divide-gray-300">
            <tbody class="divide-y divide-gray-200 py-6 my-6">
            <tr v-for="artist in filteredArtists" :key="artist.id">
              <td class="whitespace-nowrap px-3 py-4 text-3xl text-black text-center">
                <img :src="artist.avatar" alt="Artist" class="w-80 h-80 object-cover rounded-full mb-2 border-4 border-gray-400 mx-auto" />
                <div>{{ artist.artist_name }}</div>
              </td>

              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                <div v-for="album in artist.albums" :key="album.id" class="mb-4">
                  <div class="shadow-md border border-gray-300 rounded-xl p-4">
                    <img :src="album.album_image" alt="Album" class="w-60 h-60 object-cover rounded-md mb-2 border-4 border-gray-400" />
                    <div class="text-xl font-bold mb-4" style="color: rgba(31,87,74,0.99)">{{ album.album_name }} ({{ album.album_year }})</div>
                    <div class="grid grid-cols-2 gap-4">
                      <ul>
                        <li v-for="(song, index) in album.songs.slice(0, Math.ceil(album.songs.length / 2))" :key="index" class="mb-2 flex items-center">
                          <img :src="song.thumbnail_url" alt="Song" class="w-16 h-16 object-cover rounded-full border-4 border-gray-400 cursor-pointer" @click="playPauseSong(song.file, song.track_name)" />
                          <!-- Play button -->
                          <img v-if="!isSongPlaying(song.file)" src="https://cdn-icons-png.flaticon.com/512/727/727245.png" alt="Play" class="w-6 h-6 cursor-pointer ml-2" @click="playPauseSong(song.file, song.track_name)" />
                          <!-- Pause button -->
                          <img v-if="isSongPlaying(song.file)" src="https://cdn-icons-png.flaticon.com/512/566/566309.png" alt="Pause" class="w-6 h-6 cursor-pointer ml-2" @click="pauseSong(song.file)" />
                          <div class="ml-4">
                            <div class="font-semibold">{{ song.track_name }}</div>
                            <div>{{ song.genre.genre_name }}</div>
                          </div>
                        </li>
                      </ul>
                      <ul>
                        <li v-for="(song, index) in album.songs.slice(Math.ceil(album.songs.length / 2))" :key="index" class="mb-2 flex items-center">
                          <img :src="song.thumbnail_url" alt="Song" class="w-16 h-16 object-cover rounded-full border-4 border-gray-400 cursor-pointer" @click="playPauseSong(song.file, song.track_name)" />
                          <!-- Play button -->
                          <img v-if="!isSongPlaying(song.file)" src="https://cdn-icons-png.flaticon.com/512/727/727245.png" alt="Play" class="w-6 h-6 cursor-pointer ml-2" @click="playPauseSong(song.file, song.track_name)" />
                          <!-- Pause button -->
                          <img v-if="isSongPlaying(song.file)" src="https://cdn-icons-png.flaticon.com/512/566/566309.png" alt="Pause" class="w-6 h-6 cursor-pointer ml-2" @click="pauseSong(song.file)" />
                          <div class="ml-4">
                            <div class="font-semibold">{{ song.track_name }}</div>
                            <div>{{ song.genre.genre_name }}</div>
                          </div>
                        </li>
                      </ul>
                    </div>
                  </div>
                </div>
              </td>
            </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'

const searchQuery = ref('')

const artists = ref([])

onMounted(() => {
  fetch('https://2xo55fszd9.execute-api.ap-southeast-1.amazonaws.com/dev/artists')
      .then((response) => response.json())
      .then((response) => {
        console.log(response)
        artists.value = response.body
      })
      .catch((error) => {
        console.error('Error fetching artists:', error)
      })
})

const filteredArtists = computed(() => {
  const query = searchQuery.value.trim().toLowerCase()
  if (!query) return artists.value
  const filtered = artists.value.filter(artist =>
      artist.albums.some(album =>
          album.album_name.toLowerCase().includes(query)
      )
  )
  if (filtered.length === 0) {
    alert("Album doesn't exist")
  }
  return filtered
})

let currentAudio = null

const playPauseSong = (file, trackName) => {
  if (currentAudio && !currentAudio.paused && currentAudio.src === file) {
    currentAudio.pause()
    return
  }

  pauseOtherSongs()

  currentAudio = new Audio(file)
  currentAudio.play()
  console.log("Playing:", trackName)
}

const isSongPlaying = (file) => {
  return currentAudio && currentAudio.src === file && !currentAudio.paused
}

const pauseSong = (file) => {
  if (currentAudio && currentAudio.src === file) {
    currentAudio.pause()
  }
}

const pauseOtherSongs = () => {
  if (currentAudio) {
    currentAudio.pause()
  }
}
</script>

<style scoped>
.search-container {
  display: flex;
  align-items: center;
  margin: 50px; /* Margin from all sides */
}

.search-label {
  margin-right: 10px;
  color: darkgreen; /* Font color dark green */
  font-size: 24px; /* Bigger font size for the word Search */
  font-weight: bold; /* Bold font weight */
}

.search-input {
  flex: 1; /* Take remaining space */
  padding: 8px;
  border: 3px solid darkgreen; /* Border color dark green */
  border-radius: 4px;
  width: 100%; /* Set width to fill the container */
}
</style>
