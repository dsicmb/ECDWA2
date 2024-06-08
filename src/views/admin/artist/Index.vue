<template>
  <div class="px-4 sm:px-6 lg:px-8">
    <div class="sm:flex sm:items-center">
      <div class="sm:flex-auto"></div>
      <div class="mt-4 sm:ml-16 sm:mt-0 sm:flex-none">
        <RouterLink
            to="/admin/artist/create"
            type="button"
            class="block rounded-md bg-green-800 px-3 py-2 text-center text-sm font-semibold text-white shadow-sm hover:bg-white hover:text-green-800 hover:border-green-800 border-2 border-green-800 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-green-800">
          Add An Artist
        </RouterLink>
      </div>
    </div>
    <div class="mt-8 flow-root">
      <div class="-mx-4 -my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
        <div class="inline-block min-w-full py-2 align-middle sm:px-6 lg:px-8">
          <table class="min-w-full divide-y divide-gray-300">
            <thead class="bg-gray-200">
            <tr>
              <th
                  scope="col"
                  class="py-3.5 pl-4 pr-3 text-center text-base font-semibold text-green-800 sm:pl-0">
                ID
              </th>
              <th scope="col" class="px-3 py-3.5 text-left text-base font-semibold text-green-800">
                Artist Name
              </th>
              <th scope="col" class="px-3 py-3.5 text-left text-base font-semibold text-green-800">
                Avatar
              </th>
              <th scope="col" class="px-3 py-3.5 text-left text-base font-semibold text-green-800">
                Date of Birth
              </th>
              <th scope="col" class="px-3 py-3.5 text-left text-base font-semibold text-green-800">
                Country
              </th>
              <th scope="col" class="px-3 py-3.5 text-left text-base font-semibold text-green-800">
                Biography
              </th>
              <th scope="col" class="px-3 py-3.5 text-left text-base font-semibold text-green-800">
                Albums
              </th>
              <th scope="col" class="px-3 py-3.5 text-left text-base font-semibold text-green-800">
                Status
              </th>
              <th scope="col" class="relative py-3.5 pl-3 pr-4 sm:pr-0">
                <span class="sr-only">Edit</span>
              </th>
            </tr>
            </thead>

            <tbody class="divide-y divide-gray-200 py-6 my-6">
            <tr v-for="artist in artists" :key="artist.id">
              <td class="whitespace-nowrap py-4 pl-4 pr-3 text-center font-medium text-gray-900 sm:pl-0">
                  <span class="inline-block w-8 h-8 rounded-full bg-gray-200 flex items-center justify-center">
                    {{ artist.id }}
                  </span>
              </td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                {{ artist.artist_name }}
              </td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                <img
                    :src="artist.avatar"
                    alt="Artist"
                    class="w-24 h-24 object-cover rounded-full mb-2 border-4 border-gray-400"
                />
              </td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                {{ artist.birth_date }}
              </td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                {{ artist.country }}
              </td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                {{ artist.bio }}
              </td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                <div v-for="album in artist.albums" :key="album.id" class="mb-4">
                  <img
                      :src="album.album_image"
                      alt="Album"
                      class="w-16 h-16 object-cover rounded-md mb-2 border-4 border-gray-400"
                  />
                  <div>{{ album.album_name }} ({{ album.album_year }})</div>
                </div>
              </td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                <span v-if="artist.status">Active</span>
                <span v-else>Inactive</span>
              </td>
              <td class="bg-gray-200 relative whitespace-nowrap py-4 pl-3 pr-4 text-center text-l font-medium sm:pr-0">
                <RouterLink :to="`/admin/artist/${artist.id}`" class="text-green-800 hover:text-red-600 mr-4">
                  View
                </RouterLink>
                |
                <RouterLink :to="`/admin/artist/${artist.id}/edit`" class="text-green-800 hover:text-red-600 ml-4 mr-4">
                  Edit
                </RouterLink>
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

const artists = ref([]);

fetch('https://2xo55fszd9.execute-api.ap-southeast-1.amazonaws.com/dev/artists')
    .then((response) => response.json())
    .then((response) => {
      console.log(response)
      artists.value = response.body
    })


// const artists = [
//   {
//     id: 1,
//     artist_name: "Olivia Fontaine",
//     avatar: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Artist-Images/Olivia-Fontaine.jpg",
//     birth_date: "1984-12-12",
//     country: "USA",
//     bio: "Olivia Fontaine biography",
//     albums: [
//       {
//         id: 1,
//         album_name: "Echoes of Eternity",
//         album_year: 2020,
//         album_image: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Album-Images/Echoes-of-Eternity.jpg",
//         songs:[
//           {
//             id: 1,
//             track_name: "You are Enchanted",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track1.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track1.jpg",
//             genre: { id: 1, genre_name: "Pop" },
//           },
//           {
//             id: 2,
//             track_name: "They are Eternal",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track2.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track2.jpg",
//             genre: { id: 1, genre_name: "Pop" },
//           },
//           {
//             id: 3,
//             track_name: "He is Ephemeral",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track3.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track3.jpg",
//             genre: { id: 1, genre_name: "Pop" },
//           },
//           {
//             id: 4,
//             track_name: "She is Everlasting",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track4.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track4.jpg",
//             genre: { id: 1, genre_name: "Pop" },
//           },
//           {
//             id: 5,
//             track_name: "They are Endless",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track5.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track5.jpg",
//             genre: { id: 1, genre_name: "Pop" },
//           },
//           {
//             id: 6,
//             track_name: "You are my Essence",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track1.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track6.jpg",
//             genre: { id: 1, genre_name: "Pop" },
//           },
//           {
//             id: 7,
//             track_name: "They are Enigmatic",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track2.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track7.jpg",
//             genre: { id: 1, genre_name: "Pop" },
//           },
//           {
//             id: 8,
//             track_name: "He is Ethereal",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track3.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track8.jpg",
//             genre: { id: 1, genre_name: "Pop" },
//           },
//           {
//             id: 9,
//             track_name: "She is Eternal Flame",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track4.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track9.jpg",
//             genre: { id: 1, genre_name: "Pop" },
//           },
//           {
//             id: 10,
//             track_name: "They are Effervescent",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track5.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track10.jpg",
//             genre: { id: 1, genre_name: "Pop" },
//           },
//         ],
//       },
//       {
//         id: 6,
//         album_name: "Rhythm of the Cosmos",
//         album_year: 2022,
//         album_image: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Album-Images/Rhythm-of-the-Cosmos.jpg",
//         songs :[
//           {
//             id: 51,
//             track_name: "You are my Cosmic",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track1.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track1.jpg",
//             genre: { id: 1, genre_name: "Pop" },
//           },
//           {
//             id: 52,
//             track_name: "They are Celestial",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track2.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track2.jpg",
//             genre: { id: 1, genre_name: "Pop" },
//           },
//           {
//             id: 53,
//             track_name: "He is not there anymore",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track3.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track3.jpg",
//             genre: { id: 1, genre_name: "Pop" },
//           },
//           {
//             id: 54,
//             track_name: "She is Stardust",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track4.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track4.jpg",
//             genre: { id: 1, genre_name: "Pop" },
//           },
//           {
//             id: 55,
//             track_name: "They are Starlit",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track5.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track5.jpg",
//             genre: { id: 1, genre_name: "Pop" },
//           },
//           {
//             id: 56,
//             track_name: "You are my Starlight",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track1.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track6.jpg",
//             genre: { id: 1, genre_name: "Pop" },
//           },
//           {
//             id: 57,
//             track_name: "They are Stellar",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track2.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track7.jpg",
//             genre: { id: 1, genre_name: "Pop" },
//           },
//           {
//             id: 58,
//             track_name: "He is Constellation",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track3.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track8.jpg",
//             genre: { id: 1, genre_name: "Pop" },
//           },
//           {
//             id: 59,
//             track_name: "She is Solar",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track4.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track9.jpg",
//             genre: { id: 1, genre_name: "Pop" },
//           },
//           {
//             id: 60,
//             track_name: "They are Celestials",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track5.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track10.jpg",
//             genre: { id: 1, genre_name: "Pop" },
//           },
//         ],
//       }
//     ],
//     sort_order: 0,
//     status: true
//   },
//   {
//     id: 2,
//     artist_name: "Sophia Beaumont",
//     avatar: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Artist-Images/Sophia-Beaumont.jpg",
//     birth_date: "1983-10-22",
//     country: "USA",
//     bio: "Sophia Beaumont biography",
//     albums: [
//       {
//         id: 2,
//         album_name: "Midnight Serenade",
//         album_year: 2020,
//         album_image: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Album-Images/Midnight-Serenade.jpg",
//         songs :[
//           {
//             id: 11,
//             track_name: "You are my Moonlight",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track1.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track1.jpg",
//             genre: { id: 2, genre_name: "Electronic" },
//           },
//           {
//             id: 12,
//             track_name: "They are Mystical",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track2.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track2.jpg",
//             genre: { id: 2, genre_name: "Electronic" },
//           },
//           {
//             id: 13,
//             track_name: "He is Midnight",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track3.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track3.jpg",
//             genre: { id: 2, genre_name: "Electronic" },
//           },
//           {
//             id: 14,
//             track_name: "She is Serene",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track4.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track4.jpg",
//             genre: { id: 2, genre_name: "Electronic" },
//           },
//           {
//             id: 15,
//             track_name: "They are Melancholy",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track5.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track5.jpg",
//             genre: { id: 2, genre_name: "Electronic" },
//           },
//           {
//             id: 16,
//             track_name: "You are my Melody",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track1.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track6.jpg",
//             genre: { id: 2, genre_name: "Electronic" },
//           },
//           {
//             id: 17,
//             track_name: "They are Mesmerizing",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track2.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track7.jpg",
//             genre: { id: 2, genre_name: "Electronic" },
//           },
//           {
//             id: 18,
//             track_name: "He is Serenade",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track3.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track8.jpg",
//             genre: { id: 2, genre_name: "Electronic" },
//           },
//           {
//             id: 19,
//             track_name: "She is Stardust",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track4.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track9.jpg",
//             genre: { id: 2, genre_name: "Electronic" },
//           },
//           {
//             id: 20,
//             track_name: "They are Moonlit",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track5.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track10.jpg",
//             genre: { id: 2, genre_name: "Electronic" },
//           },
//         ],
//       },
//       {
//         id: 7,
//         album_name: "Melodies of the Heart",
//         album_year: 2023,
//         album_image: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Album-Images/Melodies-of-the-Heart.jpg",
//         songs :[
//           {
//             id: 61,
//             track_name: "You are my Melody",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track1.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track1.jpg",
//             genre: { id: 2, genre_name: "Electronic" },
//           },
//           {
//             id: 62,
//             track_name: "They are Melancholic",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track2.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track2.jpg",
//             genre: { id: 2, genre_name: "Electronic" },
//           },
//           {
//             id: 63,
//             track_name: "He is Heartbeat",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track3.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track3.jpg",
//             genre: { id: 2, genre_name: "Electronic" },
//           },
//           {
//             id: 64,
//             track_name: "She is Serenade",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track4.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track4.jpg",
//             genre: { id: 2, genre_name: "Electronic" },
//           },
//           {
//             id: 65,
//             track_name: "They are Soulful",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track5.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track5.jpg",
//             genre: { id: 2, genre_name: "Electronic" },
//           },
//           {
//             id: 66,
//             track_name: "You are my Serenity",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track1.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track6.jpg",
//             genre: { id: 2, genre_name: "Electronic" },
//           },
//           {
//             id: 67,
//             track_name: "They are Sentimental",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track2.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track7.jpg",
//             genre: { id: 2, genre_name: "Electronic" },
//           },
//           {
//             id: 68,
//             track_name: "He is Harmony",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track3.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track8.jpg",
//             genre: { id: 2, genre_name: "Electronic" },
//           },
//           {
//             id: 69,
//             track_name: "She is Symphony",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track4.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track9.jpg",
//             genre: { id: 2, genre_name: "Electronic" },
//           },
//           {
//             id: 70,
//             track_name: "They are Melodious",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track5.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track10.jpg",
//             genre: { id: 2, genre_name: "Electronic" },
//           },
//         ],
//       }
//     ],
//     sort_order: 0,
//     status: true
//   },
//   {
//     id: 3,
//     artist_name: "William Montgomery",
//     avatar: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Artist-Images/William-Montgomery.jpg",
//     birth_date: "1980-09-02",
//     country: "USA",
//     bio: "William Montgomery biography",
//     albums: [
//       {
//         id: 3,
//         album_name: "Whispers in the Wind",
//         album_year: 2021,
//         album_image: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Album-Images/Whispers-in-the-Wind.jpg",
//         songs :[
//           {
//             id: 21,
//             track_name: "You are my Whisper",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track1.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track1.jpg",
//             genre: { id: 3, genre_name: "Blues" },
//           },
//           {
//             id: 22,
//             track_name: "They are Whimsical",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track2.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track2.jpg",
//             genre: {id: 3, genre_name: "Blues"},
//           },
//           {
//             id: 23,
//             track_name: "He is Wind",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track3.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track3.jpg",
//             genre: { id: 3, genre_name: "Blues" },
//           },
//           {
//             id: 24,
//             track_name: "She is Sigh",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track4.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track4.jpg",
//             genre: { id: 3, genre_name: "Blues" },
//           },
//           {
//             id: 25,
//             track_name: "They are Wandering",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track5.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track5.jpg",
//             genre: { id: 3, genre_name: "Blues" },
//           },
//           {
//             id: 26,
//             track_name: "You are my Wanderlust",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track1.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track6.jpg",
//             genre: { id: 3, genre_name: "Blues" },
//           },
//           {
//             id: 27,
//             track_name: "They are Wistful",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track2.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track7.jpg",
//             genre: { id: 3, genre_name: "Blues" },
//           },
//           {
//             id: 28,
//             track_name: "He is Whispering",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track3.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track8.jpg",
//             genre: { id: 3, genre_name: "Blues" },
//           },
//           {
//             id: 29,
//             track_name: "She is Whirlwind",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track4.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track9.jpg",
//             genre: { id: 3, genre_name: "Blues" },
//           },
//           {
//             id: 30,
//             track_name: "They are Whispers",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track5.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track10.jpg",
//             genre: { id: 3, genre_name: "Blues" },
//           },
//         ],
//       },
//       {
//         id: 8,
//         album_name: "Aurora Dreams",
//         album_year: 2023,
//         album_image: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Album-Images/Aurora-Dreams.jpg",
//         songs :[
//           {
//             id: 71,
//             track_name: "You are my Aurora",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track1.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track1.jpg",
//             genre: { id: 3, genre_name: "Blues" },
//           },
//           {
//             id: 72,
//             track_name: "They are Astral",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track2.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track2.jpg",
//             genre: { id: 3, genre_name: "Blues" },
//           },
//           {
//             id: 73,
//             track_name: "He is Horizon",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track3.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track3.jpg",
//             genre: { id: 3, genre_name: "Blues" },
//           },
//           {
//             id: 74,
//             track_name: "She is Stardust",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track4.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track4.jpg",
//             genre: { id: 3, genre_name: "Blues" },
//           },
//           {
//             id: 75,
//             track_name: "They are Luminescent",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track5.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track5.jpg",
//             genre: { id: 3, genre_name: "Blues" },
//           },
//           {
//             id: 76,
//             track_name: "You are my Luminosity",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track1.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track6.jpg",
//             genre: { id: 3, genre_name: "Blues" },
//           },
//           {
//             id: 77,
//             track_name: "They are Luminous",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track2.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track7.jpg",
//             genre: { id: 3, genre_name: "Blues" },
//           },
//           {
//             id: 78,
//             track_name: "He is Twilight",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track3.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track8.jpg",
//             genre: { id: 3, genre_name: "Blues" },
//           },
//           {
//             id: 79,
//             track_name: "She is Dawn",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track4.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track9.jpg",
//             genre: { id: 3, genre_name: "Blues" },
//           },
//           {
//             id: 80,
//             track_name: "They are Dusk",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track5.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track10.jpg",
//             genre: { id: 3, genre_name: "Blues" },
//           },
//         ],
//       }
//     ],
//     sort_order: 0,
//     status: true
//   },
//   {
//     id: 4,
//     artist_name: "Benjamin Sterling",
//     avatar: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Artist-Images/Benjamin-Sterling.jpg",
//     birth_date: "1981-07-27",
//     country: "USA",
//     bio: "Benjamin Sterling biography",
//     albums: [
//       {
//         id: 4,
//         album_name: "Dreamscape Chronicles",
//         album_year: 2021,
//         album_image: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Album-Images/Dreamscape-Chronicles.jpg",
//         songs :[
//           {
//             id: 31,
//             track_name: "You are my Dreamer",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track1.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track1.jpg",
//             genre: { id: 4, genre_name: "Techno" },
//           },
//           {
//             id: 32,
//             track_name: "They are Dreaming",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track2.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track2.jpg",
//             genre: { id: 4, genre_name: "Techno" },
//           },
//           {
//             id: 33,
//             track_name: "He is Dreamcatcher",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track3.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track3.jpg",
//             genre: { id: 4, genre_name: "Techno" },
//           },
//           {
//             id: 34,
//             track_name: "She is Dreamweaver",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track4.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track4.jpg",
//             genre: { id: 4, genre_name: "Techno" },
//           },
//           {
//             id: 35,
//             track_name: "They are Dreambound",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track5.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track5.jpg",
//             genre: { id: 4, genre_name: "Techno" },
//           },
//           {
//             id: 36,
//             track_name: "You are my Dreamland",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track1.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track6.jpg",
//             genre: { id: 4, genre_name: "Techno" },
//           },
//           {
//             id: 37,
//             track_name: "They are Dreamy",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track2.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track7.jpg",
//             genre: { id: 4, genre_name: "Techno" },
//           },
//           {
//             id: 38,
//             track_name: "He is Dreaming Awake",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track3.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track8.jpg",
//             genre: { id: 4, genre_name: "Techno" },
//           },
//           {
//             id: 39,
//             track_name: "She is Dream walker",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track4.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track9.jpg",
//             genre: { id: 4, genre_name: "Techno" },
//           },
//           {
//             id: 40,
//             track_name: "They are Dreamscape",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track5.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track10.jpg",
//             genre: { id: 4, genre_name: "Techno" },
//           },
//         ],
//       },
//       {
//         id: 9,
//         album_name: "Harmony Haven",
//         album_year: 2024,
//         album_image: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Album-Images/Harmony-Haven.jpg",
//         songs :[
//           {
//             id: 81,
//             track_name: "You are my Harmony",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track1.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track1.jpg",
//             genre: { id: 4, genre_name: "Techno" },
//           },
//           {
//             id: 82,
//             track_name: "They are Harmonious",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track2.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track2.jpg",
//             genre: { id: 4, genre_name: "Techno" },
//           },
//           {
//             id: 83,
//             track_name: "He is Haven",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track3.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track3.jpg",
//             genre: { id: 4, genre_name: "Techno" },
//           },
//           {
//             id: 84,
//             track_name: "She is Sanctuary",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track4.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track4.jpg",
//             genre: { id: 4, genre_name: "Techno" },
//           },
//           {
//             id: 85,
//             track_name: "They are Serene",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track5.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track5.jpg",
//             genre: { id: 4, genre_name: "Techno" },
//           },
//           {
//             id: 86,
//             track_name: "You are my Serenity",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track1.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track6.jpg",
//             genre: { id: 4, genre_name: "Techno" },
//           },
//           {
//             id: 87,
//             track_name: "They are Tranquil",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track2.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track7.jpg",
//             genre: { id: 4, genre_name: "Techno" },
//           },
//           {
//             id: 88,
//             track_name: "He is Peace",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track3.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track8.jpg",
//             genre: { id: 4, genre_name: "Techno" },
//           },
//           {
//             id: 89,
//             track_name: "She is Calm",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track4.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track9.jpg",
//             genre: { id: 4, genre_name: "Techno" },
//           },
//           {
//             id: 90,
//             track_name: "They are Harmony",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track5.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track10.jpg",
//             genre: { id: 4, genre_name: "Techno" },
//           },
//         ],
//       }
//     ],
//     sort_order: 0,
//     status: true
//   },
//   {
//     id: 5,
//     artist_name: "Liam Sinclair",
//     avatar: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Artist-Images/Liam-Sinclair.jpg",
//     birth_date: "1988-02-02",
//     country: "USA",
//     bio: "Liam Sinclair biography",
//     albums: [
//       {
//         id: 5,
//         album_name: "Soulful Symphonies",
//         album_year: 2022,
//         album_image: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Album-Images/Soulful-Symphonies.jpg",
//         songs :[
//           {
//             id: 41,
//             track_name: "You are my Symphony",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track1.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track1.jpg",
//             genre: { id: 5, genre_name: "House" },
//           },
//           {
//             id: 42,
//             track_name: "They are Soulful",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track2.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track2.jpg",
//             genre: { id: 5, genre_name: "House" },
//           },
//           {
//             id: 43,
//             track_name: "He is Serenade",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track3.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track3.jpg",
//             genre: { id: 5, genre_name: "House" },
//           },
//           {
//             id: 44,
//             track_name: "She is Songbird",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track4.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track4.jpg",
//             genre: { id: 5, genre_name: "House" },
//           },
//           {
//             id: 45,
//             track_name: "They are Sonorous",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track5.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track5.jpg",
//             genre: { id: 5, genre_name: "House" },
//           },
//           {
//             id: 46,
//             track_name: "You are my Solace",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track1.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track6.jpg",
//             genre: { id: 5, genre_name: "House" },
//           },
//           {
//             id: 47,
//             track_name: "They are Spirited",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track2.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track7.jpg",
//             genre: { id: 5, genre_name: "House" },
//           },
//           {
//             id: 48,
//             track_name: "He is Sonata",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track3.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track8.jpg",
//             genre: { id: 5, genre_name: "House" },
//           },
//           {
//             id: 49,
//             track_name: "She is Serenity",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track4.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track9.jpg",
//             genre: { id: 5, genre_name: "House" },
//           },
//           {
//             id: 50,
//             track_name: "They are Symphonic",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track5.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track10.jpg",
//             genre: { id: 5, genre_name: "House" },
//           },
//         ],
//       },
//       {
//         id: 10,
//         album_name: "Journey Through Time",
//         album_year: 2024,
//         album_image: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Album-Images/Journey-Through-Time.jpg",
//         songs :[
//           {
//             id: 91,
//             track_name: "You are my Journey",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track1.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track1.jpg",
//             genre: { id: 5, genre_name: "House" },
//           },
//           {
//             id: 92,
//             track_name: "They are Timeless",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track2.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track2.jpg",
//             genre: { id: 5, genre_name: "House" },
//           },
//           {
//             id: 93,
//             track_name: "He is Timekeeper",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track3.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track3.jpg",
//             genre: { id: 5, genre_name: "House" },
//           },
//           {
//             id: 94,
//             track_name: "She is Time traveller",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track4.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track4.jpg",
//             genre: { id: 5, genre_name: "House" },
//           },
//           {
//             id: 95,
//             track_name: "They are Temporal",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track5.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track5.jpg",
//             genre: { id: 5, genre_name: "House" },
//           },
//           {
//             id: 96,
//             track_name: "You are my Timepiece",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track1.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track6.jpg",
//             genre: { id: 5, genre_name: "House" },
//           },
//           {
//             id: 97,
//             track_name: "They are Timebound",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track2.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track7.jpg",
//             genre: { id: 5, genre_name: "House" },
//           },
//           {
//             id: 98,
//             track_name: "He is Timeless",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track3.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track8.jpg",
//             genre: { id: 5, genre_name: "House" },
//           },
//           {
//             id: 99,
//             track_name: "She is Timekeeper",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track4.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track9.jpg",
//             genre: { id: 5, genre_name: "House" },
//           },
//           {
//             id: 100,
//             track_name: "They are Timeworn",
//             file: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Tracks/Track5.mp3",
//             thumbnail_url: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Track-Images/Track10.jpg",
//             genre: { id: 5, genre_name: "House" },
//           }
//         ],
//       }
//     ],
//     sort_order: 0,
//     status: true
//   }
// ]

</script>
<style></style>
