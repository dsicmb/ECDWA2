<template>
  <div class="px-4 sm:px-6 lg:px-8">
    <div class="sm:flex sm:items-center">
      <div class="sm:flex-auto">
        <!-- Any content here -->
      </div>
      <div class="mt-4 sm:ml-16 sm:mt-0 sm:flex-none">
        <RouterLink
            to="/admin/track/create"
            type="button"
            class="block rounded-md bg-green-800 px-3 py-2 text-center text-sm font-semibold text-white shadow-sm
          hover:bg-white hover:text-green-800 hover:border-green-800
          border-2 border-green-800 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2
          focus-visible:outline-green-800">
          Add A Track
        </RouterLink>
      </div>
    </div>
    <div class="mt-8 flow-root">
      <div class="-mx-4 -my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
        <div class="inline-block min-w-full py-2 align-middle sm:px-6 lg:px-8">
          <table class="min-w-full divide-y divide-gray-300">
            <thead class="bg-gray-200">
            <tr>
              <th scope="col" class="py-3.5 pl-4 pr-3 text-center text-base font-semibold text-green-800 sm:pl-0">ID</th>
              <th scope="col" class="px-3 py-3.5 text-left text-base font-semibold text-green-800">Name of the Track</th>
              <th scope="col" class="px-3 py-3.5 text-left text-base font-semibold text-green-800">File</th>
              <th scope="col" class="px-3 py-3.5 text-left text-base font-semibold text-green-800">Genre</th>
              <th scope="col" class="px-3 py-3.5 text-left text-base font-semibold text-green-800">Duration</th>
              <th scope="col" class="px-3 py-3.5 text-left text-base font-semibold text-green-800">Artist</th>
              <th scope="col" class="px-3 py-3.5 text-left text-base font-semibold text-green-800">Album</th>
              <th scope="col" class="px-3 py-3.5 text-left text-base font-semibold text-green-800">Status</th>
              <th scope="col" class="relative py-3.5 pl-3 pr-4 sm:pr-0"><span class="sr-only">Edit</span></th>
            </tr>
            </thead>
            <tbody class="divide-y divide-gray-200">
            <tr v-for="track in tracks" :key="track.id">
              <td class="whitespace-nowrap py-4 pl-4 pr-3 text-center font-medium text-gray-900 sm:pl-0">
                <span class="inline-block w-8 h-8 rounded-full bg-gray-200 flex items-center justify-center">
                  {{ track.id }}</span>
              </td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">{{ track.track_name }}</td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">

                <RouterLink :to="`/admin/track/${track.id}`" class="group text-green-800 hover:text-red-600 mr-4">
                  <div class="relative w-16 h-16">
                    <img
                        :src="track.thumbnail_url"
                        alt="Track"
                        class="w-full h-full object-cover rounded-full border-4 border-gray-400 group-hover:border-green-800"/>
                    <div class="absolute inset-0 flex items-center justify-center">
                      <svg
                          class="w-8 h-8 text-white fill-current group-hover:text-gray-300"
                          xmlns="http://www.w3.org/2000/svg"
                          viewBox="0 0 24 24">
                        <path d="M8 5v14l11-7z"/>
                      </svg>
                    </div>
                  </div>
                </RouterLink>

                <!-- <audio controls :src="track.file" class="w-full mt-2"></audio> -->
              </td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">{{ track.genre.genre_name }}</td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">{{ track.track_duration }}</td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">{{ track.artist.artist_name }}</td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">{{ track.album.album_name }}</td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                <span v-if="track.status">Active</span>
                <span v-else>Inactive</span>
              </td>
              <td class="bg-gray-200 relative whitespace-nowrap py-4 pl-3 pr-4 text-center text-l font-medium sm:pr-0">
                <RouterLink :to="`/admin/track/${track.id}`" class="text-green-800 hover:text-red-600 mr-4">View</RouterLink>|
                <RouterLink :to="`/admin/track/${track.id}/edit`" class="text-green-800 hover:text-red-600 ml-4 mr-4">Edit</RouterLink>
              </td>
            </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
  <router-view />
</template>

<script setup>

import { ref } from 'vue';
import { RouterLink } from 'vue-router';

const tracks = ref([]);

fetch('https://2xo55fszd9.execute-api.ap-southeast-1.amazonaws.com/dev/tracks')
    .then((response) => response.json())
    .then((response) => {
      console.log(response)
      tracks.value = response.body
    })

// const tracks = [
//   {
//     id: 1,
//     track_name: "You are Enchanted",
//     file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track1.mp3",
//     thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track1.jpg",
//     genre: { id: 1, genre_name: "Pop" },
//     track_duration: 187,
//     artist: { id: 1, artist_name : 'Olivia Fontaine' },
//     album: { id: 1, album_name: "Echoes of Eternity" },
//     sort_order: 0,
//     status: true
//   },
//   {
//     id: 2,
//     track_name: "They are Eternal",
//     file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track2.mp3",
//     thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track2.jpg",
//     genre: { id: 1, genre_name: "Pop" },
//     track_duration: 183,
//     artist: { id: 1, artist_name : 'Olivia Fontaine' },
//     album: { id: 1, album_name: "Echoes of Eternity" },
//     sort_order: 0,
//     status: true
//   },
//   {
//     id: 3,
//     track_name: "He is Ephemeral",
//     file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track3.mp3",
//     thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track3.jpg",
//     genre: { id: 1, genre_name: "Pop" },
//     track_duration: 185,
//     artist: { id: 1, artist_name : 'Olivia Fontaine' },
//     album: { id: 1, album_name: "Echoes of Eternity" },
//     sort_order: 0,
//     status: true
//   },
//   {
//     id: 4,
//     track_name: "She is Everlasting",
//     file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track4.mp3",
//     thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track4.jpg",
//     genre: { id: 1, genre_name: "Pop" },
//     track_duration: 184,
//     artist: { id: 1, artist_name : 'Olivia Fontaine' },
//     album: { id: 1, album_name: "Echoes of Eternity" },
//     sort_order: 0,
//     status: true
//   },
//   {
//     id: 5,
//     track_name: "They are Endless",
//     file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track4.mp3",
//     thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track5.jpg",
//     genre: { id: 1, genre_name: "Pop" },
//     track_duration: 186,
//     artist: { id: 1, artist_name : 'Olivia Fontaine' },
//     album: { id: 1, album_name: "Echoes of Eternity" },
//     sort_order: 0,
//     status: true
//   },
//   {
//     id: 6,
//     track_name: "You are my Essence",
//     file: "FILE_PATH",
//     thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track6.jpg",
//     genre: { id: 1, genre_name: "Pop" },
//     track_duration: 182,
//     artist: { id: 1, artist_name : 'Olivia Fontaine' },
//     album: { id: 1, album_name: "Echoes of Eternity" },
//     sort_order: 0,
//     status: true
//   },
//   {
//     id: 7,
//     track_name: "They are Enigmatic",
//     file: "FILE_PATH",
//     thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track7.jpg",
//     genre: { id: 1, genre_name: "Pop" },
//     track_duration: 181,
//     artist: { id: 1, artist_name : 'Olivia Fontaine' },
//     album: { id: 1, album_name: "Echoes of Eternity" },
//     sort_order: 0,
//     status: true
//   },
//   {
//     id: 8,
//     track_name: "He is Ethereal",
//     file: "FILE_PATH",
//     thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track8.jpg",
//     genre: { id: 1, genre_name: "Pop" },
//     track_duration: 187,
//     artist: { id: 1, artist_name : 'Olivia Fontaine' },
//     album: { id: 1, album_name: "Echoes of Eternity" },
//     sort_order: 0,
//     status: true
//   },
//   {
//     id: 9,
//     track_name: "She is Eternal Flame",
//     file: "FILE_PATH",
//     thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track9.jpg",
//     genre: { id: 1, genre_name: "Pop" },
//     track_duration: 186,
//     artist: { id: 1, artist_name : 'Olivia Fontaine' },
//     album: { id: 1, album_name: "Echoes of Eternity" },
//     sort_order: 0,
//     status: true
//   },
//   {
//     id: 10,
//     track_name: "They are Effervescent",
//     file: "FILE_PATH",
//     thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track10.jpg",
//     genre: { id: 1, genre_name: "Pop" },
//     track_duration: 183,
//     artist: { id: 1, artist_name : 'Olivia Fontaine' },
//     album: { id: 1, album_name: "Echoes of Eternity" },
//     sort_order: 0,
//     status: true
//   },
//     {
//       id: 11,
//       track_name: "You are my Moonlight",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track1.jpg",
//       genre: { id: 2, genre_name: "Electronic" },
//       track_duration: 184,
//       artist: { id: 2, artist_name : 'Sophia Beaumont' },
//       album: { id: 2, album_name: "Midnight Serenade" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 12,
//       track_name: "They are Mystical",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track2.jpg",
//       genre: { id: 2, genre_name: "Electronic" },
//       track_duration: 186,
//       artist: { id: 2, artist_name : 'Sophia Beaumont' },
//       album: { id: 2, album_name: "Midnight Serenade" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 13,
//       track_name: "He is Midnight",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track3.jpg",
//       genre: { id: 2, genre_name: "Electronic" },
//       track_duration: 182,
//       artist: { id: 2, artist_name : 'Sophia Beaumont' },
//       album: { id: 2, album_name: "Midnight Serenade" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 14,
//       track_name: "She is Serene",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track4.jpg",
//       genre: { id: 2, genre_name: "Electronic" },
//       track_duration: 187,
//       artist: { id: 2, artist_name : 'Sophia Beaumont' },
//       album: { id: 2, album_name: "Midnight Serenade" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 15,
//       track_name: "They are Melancholy",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track5.jpg",
//       genre: { id: 2, genre_name: "Electronic" },
//       track_duration: 185,
//       artist: { id: 2, artist_name : 'Sophia Beaumont' },
//       album: { id: 2, album_name: "Midnight Serenade" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 16,
//       track_name: "You are my Melody",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track6.jpg",
//       genre: { id: 2, genre_name: "Electronic" },
//       track_duration: 183,
//       artist: { id: 2, artist_name : 'Sophia Beaumont' },
//       album: { id: 2, album_name: "Midnight Serenade" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 17,
//       track_name: "They are Mesmerizing",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track7.jpg",
//       genre: { id: 2, genre_name: "Electronic" },
//       track_duration: 184,
//       artist: { id: 2, artist_name : 'Sophia Beaumont' },
//       album: { id: 2, album_name: "Midnight Serenade" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 18,
//       track_name: "He is Serenade",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track8.jpg",
//       genre: { id: 2, genre_name: "Electronic" },
//       track_duration: 187,
//       artist: { id: 2, artist_name : 'Sophia Beaumont' },
//       album: { id: 2, album_name: "Midnight Serenade" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 19,
//       track_name: "She is Stardust",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track9.jpg",
//       genre: { id: 2, genre_name: "Electronic" },
//       track_duration: 182,
//       artist: { id: 2, artist_name : 'Sophia Beaumont' },
//       album: { id: 2, album_name: "Midnight Serenade" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 20,
//       track_name: "They are Moonlit",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track10.jpg",
//       genre: { id: 2, genre_name: "Electronic" },
//       track_duration: 183,
//       artist: { id: 2, artist_name : 'Sophia Beaumont' },
//       album: { id: 2, album_name: "Midnight Serenade" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 21,
//       track_name: "You are my Whisper",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track1.jpg",
//       genre: { id: 3, genre_name: "Blues" },
//       track_duration: 185,
//       artist: { id: 3, artist_name : 'William Montgomery' },
//       album: { id: 3, album_name: "Whispers in the Wind" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 22,
//       track_name: "They are Whimsical",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track2.jpg",
//       genre: { id: 3, genre_name: "Blues" },
//       track_duration: 182,
//       artist: { id: 3, artist_name : 'William Montgomery' },
//       album: { id: 3, album_name: "Whispers in the Wind" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 23,
//       track_name: "He is Wind",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track3.jpg",
//       genre: { id: 3, genre_name: "Blues" },
//       track_duration: 184,
//       artist: { id: 3, artist_name : 'William Montgomery' },
//       album: { id: 3, album_name: "Whispers in the Wind" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 24,
//       track_name: "She is Sigh",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track4.jpg",
//       genre: { id: 3, genre_name: "Blues" },
//       track_duration: 186,
//       artist: { id: 3, artist_name : 'William Montgomery' },
//       album: { id: 3, album_name: "Whispers in the Wind" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 25,
//       track_name: "They are Wandering",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track5.jpg",
//       genre: { id: 3, genre_name: "Blues" },
//       track_duration: 185,
//       artist: { id: 3, artist_name : 'William Montgomery' },
//       album: { id: 3, album_name: "Whispers in the Wind" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 26,
//       track_name: "You are my Wanderlust",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track6.jpg",
//       genre: { id: 3, genre_name: "Blues" },
//       track_duration: 183,
//       artist: { id: 3, artist_name : 'William Montgomery' },
//       album: { id: 3, album_name: "Whispers in the Wind" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 27,
//       track_name: "They are Wistful",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track7.jpg",
//       genre: { id: 3, genre_name: "Blues" },
//       track_duration: 186,
//       artist: { id: 3, artist_name : 'William Montgomery' },
//       album: { id: 3, album_name: "Whispers in the Wind" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 28,
//       track_name: "He is Whispering",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track8.jpg",
//       genre: { id: 3, genre_name: "Blues" },
//       track_duration: 184,
//       artist: { id: 3, artist_name : 'William Montgomery' },
//       album: { id: 3, album_name: "Whispers in the Wind" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 29,
//       track_name: "She is Whirlwind",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track9.jpg",
//       genre: { id: 3, genre_name: "Blues" },
//       track_duration: 182,
//       artist: { id: 3, artist_name : 'William Montgomery' },
//       album: { id: 3, album_name: "Whispers in the Wind" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 30,
//       track_name: "They are Whispers",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track10.jpg",
//       genre: { id: 3, genre_name: "Blues" },
//       track_duration: 187,
//       artist: { id: 3, artist_name : 'William Montgomery' },
//       album: { id: 3, album_name: "Whispers in the Wind" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 31,
//       track_name: "You are my Dreamer",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track1.jpg",
//       genre: { id: 4, genre_name: "Techno" },
//       track_duration: 182,
//       artist: { id: 4, artist_name : 'Benjamin Sterling' },
//       album: { id: 4, album_name: "Dreamscape Chronicles" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 32,
//       track_name: "They are Dreaming",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track2.jpg",
//       genre: { id: 4, genre_name: "Techno" },
//       track_duration: 187,
//       artist: { id: 4, artist_name : 'Benjamin Sterling' },
//       album: { id: 4, album_name: "Dreamscape Chronicles" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 33,
//       track_name: "He is Dreamcatcher",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track3.jpg",
//       genre: { id: 4, genre_name: "Techno" },
//       track_duration: 185,
//       artist: { id: 4, artist_name : 'Benjamin Sterling' },
//       album: { id: 4, album_name: "Dreamscape Chronicles" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 34,
//       track_name: "She is Dreamweaver",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track4.jpg",
//       genre: { id: 4, genre_name: "Techno" },
//       track_duration: 183,
//       artist: { id: 4, artist_name : 'Benjamin Sterling' },
//       album: { id: 4, album_name: "Dreamscape Chronicles" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 35,
//       track_name: "They are Dreambound",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track5.jpg",
//       genre: { id: 4, genre_name: "Techno" },
//       track_duration: 186,
//       artist: { id: 4, artist_name : 'Benjamin Sterling' },
//       album: { id: 4, album_name: "Dreamscape Chronicles" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 36,
//       track_name: "You are my Dreamland",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track6.jpg",
//       genre: { id: 4, genre_name: "Techno" },
//       track_duration: 183,
//       artist: { id: 4, artist_name : 'Benjamin Sterling' },
//       album: { id: 4, album_name: "Dreamscape Chronicles" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 37,
//       track_name: "They are Dreamy",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track7.jpg",
//       genre: { id: 4, genre_name: "Techno" },
//       track_duration: 184,
//       artist: { id: 4, artist_name : 'Benjamin Sterling' },
//       album: { id: 4, album_name: "Dreamscape Chronicles" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 38,
//       track_name: "He is Dreaming Awake",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track8.jpg",
//       genre: { id: 4, genre_name: "Techno" },
//       track_duration: 182,
//       artist: { id: 4, artist_name : 'Benjamin Sterling' },
//       album: { id: 4, album_name: "Dreamscape Chronicles" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 39,
//       track_name: "She is Dream walker",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track9.jpg",
//       genre: { id: 4, genre_name: "Techno" },
//       track_duration: 187,
//       artist: { id: 4, artist_name : 'Benjamin Sterling' },
//       album: { id: 4, album_name: "Dreamscape Chronicles" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 40,
//       track_name: "They are Dreamscape",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track10.jpg",
//       genre: { id: 4, genre_name: "Techno" },
//       track_duration: 185,
//       artist: { id: 4, artist_name : 'Benjamin Sterling' },
//       album: { id: 4, album_name: "Dreamscape Chronicles" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 41,
//       track_name: "You are my Symphony",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track1.jpg",
//       genre: { id: 5, genre_name: "House" },
//       track_duration: 186,
//       artist: { id: 5, artist_name : 'Liam Sinclair' },
//       album: { id: 5, album_name: "Soulful Symphonies" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 42,
//       track_name: "They are Soulful",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track2.jpg",
//       genre: { id: 5, genre_name: "House" },
//       track_duration: 184,
//       artist: { id: 5, artist_name : 'Liam Sinclair' },
//       album: { id: 5, album_name: "Soulful Symphonies" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 43,
//       track_name: "He is Serenade",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track3.jpg",
//       genre: { id: 5, genre_name: "House" },
//       track_duration: 182,
//       artist: { id: 5, artist_name : 'Liam Sinclair' },
//       album: { id: 5, album_name: "Soulful Symphonies" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 44,
//       track_name: "She is Songbird",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track4.jpg",
//       genre: { id: 5, genre_name: "House" },
//       track_duration: 185,
//       artist: { id: 5, artist_name : 'Liam Sinclair' },
//       album: { id: 5, album_name: "Soulful Symphonies" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 45,
//       track_name: "They are Sonorous",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track5.jpg",
//       genre: { id: 5, genre_name: "House" },
//       track_duration: 183,
//       artist: { id: 5, artist_name : 'Liam Sinclair' },
//       album: { id: 5, album_name: "Soulful Symphonies" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 46,
//       track_name: "You are my Solace",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track6.jpg",
//       genre: { id: 5, genre_name: "House" },
//       track_duration: 187,
//       artist: { id: 5, artist_name : 'Liam Sinclair' },
//       album: { id: 5, album_name: "Soulful Symphonies" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 47,
//       track_name: "They are Spirited",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track7.jpg",
//       genre: { id: 5, genre_name: "House" },
//       track_duration: 184,
//       artist: { id: 5, artist_name : 'Liam Sinclair' },
//       album: { id: 5, album_name: "Soulful Symphonies" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 48,
//       track_name: "He is Sonata",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track8.jpg",
//       genre: { id: 5, genre_name: "House" },
//       track_duration: 186,
//       artist: { id: 5, artist_name : 'Liam Sinclair' },
//       album: { id: 5, album_name: "Soulful Symphonies" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 49,
//       track_name: "She is Serenity",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track9.jpg",
//       genre: { id: 5, genre_name: "House" },
//       track_duration: 182,
//       artist: { id: 5, artist_name : 'Liam Sinclair' },
//       album: { id: 5, album_name: "Soulful Symphonies" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 50,
//       track_name: "They are Symphonic",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track10.jpg",
//       genre: { id: 5, genre_name: "House" },
//       track_duration: 185,
//       artist: { id: 5, artist_name : 'Liam Sinclair' },
//       album: { id: 5, album_name: "Soulful Symphonies" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 51,
//       track_name: "You are my Cosmic",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track1.jpg",
//       genre: { id: 1, genre_name: "Pop" },
//       track_duration: 187,
//       artist: { id: 1, artist_name : 'Olivia Fontaine' },
//       album: { id: 6, album_name: "Rhythm of the Cosmos" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 52,
//       track_name: "They are Celestial",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track2.jpg",
//       genre: { id: 1, genre_name: "Pop" },
//       track_duration: 186,
//       artist: { id: 1, artist_name : 'Olivia Fontaine' },
//       album: { id: 6, album_name: "Rhythm of the Cosmos" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 53,
//       track_name: "He is not there anymore",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track3.jpg",
//       genre: { id: 1, genre_name: "Pop" },
//       track_duration: 183,
//       artist: { id: 1, artist_name : 'Olivia Fontaine' },
//       album: { id: 6, album_name: "Rhythm of the Cosmos" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 54,
//       track_name: "She is Stardust",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track4.jpg",
//       genre: { id: 1, genre_name: "Pop" },
//       track_duration: 185,
//       artist: { id: 1, artist_name : 'Olivia Fontaine' },
//       album: { id: 6, album_name: "Rhythm of the Cosmos" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 55,
//       track_name: "They are Starlit",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track5.jpg",
//       genre: { id: 1, genre_name: "Pop" },
//       track_duration: 182,
//       artist: { id: 1, artist_name : 'Olivia Fontaine' },
//       album: { id: 6, album_name: "Rhythm of the Cosmos" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 56,
//       track_name: "You are my Starlight",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track6.jpg",
//       genre: { id: 1, genre_name: "Pop" },
//       track_duration: 184,
//       artist: { id: 1, artist_name : 'Olivia Fontaine' },
//       album: { id: 6, album_name: "Rhythm of the Cosmos" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 57,
//       track_name: "They are Stellar",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track7.jpg",
//       genre: { id: 1, genre_name: "Pop" },
//       track_duration: 187,
//       artist: { id: 1, artist_name : 'Olivia Fontaine' },
//       album: { id: 6, album_name: "Rhythm of the Cosmos" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 58,
//       track_name: "He is Constellation",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track8.jpg",
//       genre: { id: 1, genre_name: "Pop" },
//       track_duration: 185,
//       artist: { id: 1, artist_name : 'Olivia Fontaine' },
//       album: { id: 6, album_name: "Rhythm of the Cosmos" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 59,
//       track_name: "She is Solar",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track9.jpg",
//       genre: { id: 1, genre_name: "Pop" },
//       track_duration: 183,
//       artist: { id: 1, artist_name : 'Olivia Fontaine' },
//       album: { id: 6, album_name: "Rhythm of the Cosmos" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 60,
//       track_name: "They are Celestials",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track10.jpg",
//       genre: { id: 1, genre_name: "Pop" },
//       track_duration: 184,
//       artist: { id: 1, artist_name : 'Olivia Fontaine' },
//       album: { id: 6, album_name: "Rhythm of the Cosmos" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 61,
//       track_name: "You are my Melody",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track1.jpg",
//       genre: { id: 2, genre_name: "Electronic" },
//       track_duration: 183,
//       artist: { id: 2, artist_name : 'Sophia Beaumont' },
//       album: { id: 7, album_name: "Melodies of the Heart" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 62,
//       track_name: "They are Melancholic",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track2.jpg",
//       genre: { id: 2, genre_name: "Electronic" },
//       track_duration: 185,
//       artist: { id: 2, artist_name : 'Sophia Beaumont' },
//       album: { id: 7, album_name: "Melodies of the Heart" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 63,
//       track_name: "He is Heartbeat",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track3.jpg",
//       genre: { id: 2, genre_name: "Electronic" },
//       track_duration: 184,
//       artist: { id: 2, artist_name : 'Sophia Beaumont' },
//       album: { id: 7, album_name: "Melodies of the Heart" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 64,
//       track_name: "She is Serenade",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track4.jpg",
//       genre: { id: 2, genre_name: "Electronic" },
//       track_duration: 182,
//       artist: { id: 2, artist_name : 'Sophia Beaumont' },
//       album: { id: 7, album_name: "Melodies of the Heart" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 65,
//       track_name: "They are Soulful",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track5.jpg",
//       genre: { id: 2, genre_name: "Electronic" },
//       track_duration: 187,
//       artist: { id: 2, artist_name : 'Sophia Beaumont' },
//       album: { id: 7, album_name: "Melodies of the Heart" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 66,
//       track_name: "You are my Serenity",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track6.jpg",
//       genre: { id: 2, genre_name: "Electronic" },
//       track_duration: 183,
//       artist: { id: 2, artist_name : 'Sophia Beaumont' },
//       album: { id: 7, album_name: "Melodies of the Heart" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 67,
//       track_name: "They are Sentimental",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track7.jpg",
//       genre: { id: 2, genre_name: "Electronic" },
//       track_duration: 186,
//       artist: { id: 2, artist_name : 'Sophia Beaumont' },
//       album: { id: 7, album_name: "Melodies of the Heart" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 68,
//       track_name: "He is Harmony",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track8.jpg",
//       genre: { id: 2, genre_name: "Electronic" },
//       track_duration: 184,
//       artist: { id: 2, artist_name : 'Sophia Beaumont' },
//       album: { id: 7, album_name: "Melodies of the Heart" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 69,
//       track_name: "She is Symphony",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track9.jpg",
//       genre: { id: 2, genre_name: "Electronic" },
//       track_duration: 182,
//       artist: { id: 2, artist_name : 'Sophia Beaumont' },
//       album: { id: 7, album_name: "Melodies of the Heart" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 70,
//       track_name: "They are Melodious",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track10.jpg",
//       genre: { id: 2, genre_name: "Electronic" },
//       track_duration: 185,
//       artist: { id: 2, artist_name : 'Sophia Beaumont' },
//       album: { id: 7, album_name: "Melodies of the Heart" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 71,
//       track_name: "You are my Aurora",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track1.jpg",
//       genre: { id: 3, genre_name: "Blues" },
//       track_duration: 183,
//       artist: { id: 3, artist_name : 'William Montgomery' },
//       album: { id: 8, album_name: "Aurora Dreams" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 72,
//       track_name: "They are Astral",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track2.jpg",
//       genre: { id: 3, genre_name: "Blues" },
//       track_duration: 186,
//       artist: { id: 3, artist_name : 'William Montgomery' },
//       album: { id: 8, album_name: "Aurora Dreams" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 73,
//       track_name: "He is Horizon",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track3.jpg",
//       genre: { id: 3, genre_name: "Blues" },
//       track_duration: 187,
//       artist: { id: 3, artist_name : 'William Montgomery' },
//       album: { id: 8, album_name: "Aurora Dreams" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 74,
//       track_name: "She is Stardust",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track4.jpg",
//       genre: { id: 3, genre_name: "Blues" },
//       track_duration: 182,
//       artist: { id: 3, artist_name : 'William Montgomery' },
//       album: { id: 8, album_name: "Aurora Dreams" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 75,
//       track_name: "They are Luminescent",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track5.jpg",
//       genre: { id: 3, genre_name: "Blues" },
//       track_duration: 189,
//       artist: { id: 3, artist_name : 'William Montgomery' },
//       album: { id: 8, album_name: "Aurora Dreams" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 76,
//       track_name: "You are my Luminosity",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track6.jpg",
//       genre: { id: 3, genre_name: "Blues" },
//       track_duration: 184,
//       artist: { id: 3, artist_name : 'William Montgomery' },
//       album: { id: 8, album_name: "Aurora Dreams" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 77,
//       track_name: "They are Luminous",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track7.jpg",
//       genre: { id: 3, genre_name: "Blues" },
//       track_duration: 181,
//       artist: { id: 3, artist_name : 'William Montgomery' },
//       album: { id: 8, album_name: "Aurora Dreams" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 78,
//       track_name: "He is Twilight",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track8.jpg",
//       genre: { id: 3, genre_name: "Blues" },
//       track_duration: 186,
//       artist: { id: 3, artist_name : 'William Montgomery' },
//       album: { id: 8, album_name: "Aurora Dreams" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 79,
//       track_name: "She is Dawn",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track9.jpg",
//       genre: { id: 3, genre_name: "Blues" },
//       track_duration: 183,
//       artist: { id: 3, artist_name : 'William Montgomery' },
//       album: { id: 8, album_name: "Aurora Dreams" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 80,
//       track_name: "They are Dusk",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track10.jpg",
//       genre: { id: 3, genre_name: "Blues" },
//       track_duration: 185,
//       artist: { id: 3, artist_name : 'William Montgomery' },
//       album: { id: 8, album_name: "Aurora Dreams" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 81,
//       track_name: "You are my Harmony",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track1.jpg",
//       genre: { id: 4, genre_name: "Techno" },
//       track_duration: 182,
//       artist: { id: 4, artist_name : 'Benjamin Sterling' },
//       album: { id: 9, album_name: "Harmony Haven" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 82,
//       track_name: "They are Harmonious",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track2.jpg",
//       genre: { id: 4, genre_name: "Techno" },
//       track_duration: 183,
//       artist: { id: 4, artist_name : 'Benjamin Sterling' },
//       album: { id: 9, album_name: "Harmony Haven" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 83,
//       track_name: "He is Haven",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track3.jpg",
//       genre: { id: 4, genre_name: "Techno" },
//       track_duration: 185,
//       artist: { id: 4, artist_name : 'Benjamin Sterling' },
//       album: { id: 9, album_name: "Harmony Haven" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 84,
//       track_name: "She is Sanctuary",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track4.jpg",
//       genre: { id: 4, genre_name: "Techno" },
//       track_duration: 181,
//       artist: { id: 4, artist_name : 'Benjamin Sterling' },
//       album: { id: 9, album_name: "Harmony Haven" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 85,
//       track_name: "They are Serene",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track5.jpg",
//       genre: { id: 4, genre_name: "Techno" },
//       track_duration: 181,
//       artist: { id: 4, artist_name : 'Benjamin Sterling' },
//       album: { id: 9, album_name: "Harmony Haven" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 86,
//       track_name: "You are my Serenity",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track6.jpg",
//       genre: { id: 4, genre_name: "Techno" },
//       track_duration: 183,
//       artist: { id: 4, artist_name : 'Benjamin Sterling' },
//       album: { id: 9, album_name: "Harmony Haven" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 87,
//       track_name: "They are Tranquil",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track7.jpg",
//       genre: { id: 4, genre_name: "Techno" },
//       track_duration: 189,
//       artist: { id: 4, artist_name : 'Benjamin Sterling' },
//       album: { id: 9, album_name: "Harmony Haven" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 88,
//       track_name: "He is Peace",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track8.jpg",
//       genre: { id: 4, genre_name: "Techno" },
//       track_duration: 183,
//       artist: { id: 4, artist_name : 'Benjamin Sterling' },
//       album: { id: 9, album_name: "Harmony Haven" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 89,
//       track_name: "She is Calm",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track9.jpg",
//       genre: { id: 4, genre_name: "Techno" },
//       track_duration: 182,
//       artist: { id: 4, artist_name : 'Benjamin Sterling' },
//       album: { id: 9, album_name: "Harmony Haven" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 90,
//       track_name: "They are Harmony",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track10.jpg",
//       genre: { id: 4, genre_name: "Techno" },
//       track_duration: 185,
//       artist: { id: 4, artist_name : 'Benjamin Sterling' },
//       album: { id: 9, album_name: "Harmony Haven" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 91,
//       track_name: "You are my Journey",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track1.jpg",
//       genre: { id: 5, genre_name: "House" },
//       track_duration: 182,
//       artist: { id: 5, artist_name : 'Liam Sinclair' },
//       album: { id: 10, album_name: "Journey Through Time" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 92,
//       track_name: "They are Timeless",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track2.jpg",
//       genre: { id: 5, genre_name: "House" },
//       track_duration: 185,
//       artist: { id: 5, artist_name : 'Liam Sinclair' },
//       album: { id: 10, album_name: "Journey Through Time" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 93,
//       track_name: "He is Timekeeper",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track3.jpg",
//       genre: { id: 5, genre_name: "House" },
//       track_duration: 183,
//       artist: { id: 5, artist_name : 'Liam Sinclair' },
//       album: { id: 10, album_name: "Journey Through Time" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 94,
//       track_name: "She is Time traveller",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track4.jpg",
//       genre: { id: 5, genre_name: "House" },
//       track_duration: 188,
//       artist: { id: 5, artist_name : 'Liam Sinclair' },
//       album: { id: 10, album_name: "Journey Through Time" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 95,
//       track_name: "They are Temporal",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track5.jpg",
//       genre: { id: 5, genre_name: "House" },
//       track_duration: 181,
//       artist: { id: 5, artist_name : 'Liam Sinclair' },
//       album: { id: 10, album_name: "Journey Through Time" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 96,
//       track_name: "You are my Timepiece",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track6.jpg",
//       genre: { id: 5, genre_name: "House" },
//       track_duration: 181,
//       artist: { id: 5, artist_name : 'Liam Sinclair' },
//       album: { id: 10, album_name: "Journey Through Time" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 97,
//       track_name: "They are Timebound",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track7.jpg",
//       genre: { id: 5, genre_name: "House" },
//       track_duration: 189,
//       artist: { id: 5, artist_name : 'Liam Sinclair' },
//       album: { id: 10, album_name: "Journey Through Time" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 98,
//       track_name: "He is Timeless",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track8.jpg",
//       genre: { id: 5, genre_name: "House" },
//       track_duration: 184,
//       artist: { id: 5, artist_name : 'Liam Sinclair' },
//       album: { id: 10, album_name: "Journey Through Time" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 99,
//       track_name: "She is Timekeeper",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track9.jpg",
//       genre: { id: 5, genre_name: "House" },
//       track_duration: 182,
//       artist: { id: 5, artist_name : 'Liam Sinclair' },
//       album: { id: 10, album_name: "Journey Through Time" },
//       sort_order: 0,
//       status: true
//     },
//     {
//       id: 100,
//       track_name: "They are Timeworn",
//       file: "FILE_PATH",
//       thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track10.jpg",
//       genre: { id: 5, genre_name: "House" },
//       track_duration: 181,
//       artist: { id: 5, artist_name : 'Liam Sinclair' },
//       album: { id: 10, album_name: "Journey Through Time" },
//       sort_order: 0,
//       status: true
//     }
// ]
</script>
<style></style>
