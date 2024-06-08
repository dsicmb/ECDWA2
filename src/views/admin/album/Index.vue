<template>
  <div class="px-4 sm:px-6 lg:px-8">
    <div class="sm:flex sm:items-center">
      <div class="sm:flex-auto">
      </div>
      <div class="mt-4 sm:ml-16 sm:mt-0 sm:flex-none">
        <div class="flex">
          <RouterLink
              to="/admin/album/create"
              type="button"
              class="block rounded-md bg-green-800 px-3 py-2 text-center text-sm font-semibold text-white shadow-sm
      hover:bg-white hover:text-green-800 hover:border-green-800
      border-2 border-green-800 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2
      focus-visible:outline-green-800 mr-2">
            Add An Album
          </RouterLink>
        </div>
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
                Album Name
              </th>
              <th scope="col" class="px-3 py-3.5 text-left text-base font-semibold text-green-800">
                Artist Name
              </th>
              <th scope="col" class="px-3 py-3.5 text-left text-base font-semibold text-green-800">
                Genre Name
              </th>
              <th scope="col" class="px-3 py-3.5 text-left text-base font-semibold text-green-800">
                Tracks
              </th>
              <th scope="col" class="px-3 py-3.5 text-left text-base font-semibold text-green-800">
                Year
              </th>
              <th scope="col" class="px-3 py-3.5 text-left text-base font-semibold text-green-800">
                Studio
              </th>
              <th scope="col" class="px-3 py-3.5 text-left text-base font-semibold text-green-800">
                Producer
              </th>
              <th scope="col" class="px-3 py-3.5 text-left text-base font-semibold text-green-800">
                Status
              </th>

              <th scope="col" class="relative py-3.5 pl-3 pr-4 sm:pr-0">
                <span class="sr-only">Edit</span>
              </th>
            </tr>
            </thead>
            <tbody class="divide-y divide-gray-200">
            <tr v-for="album in albums" :key="album.id">
              <td class="whitespace-nowrap py-4 pl-4 pr-3 text-center font-medium text-gray-900 sm:pl-0">
                <span class="inline-block w-8 h-8 rounded-full bg-gray-200 flex items-center justify-center">
                  {{ album.id }}</span>
              </td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                <img :src="album.album_image" alt="Album Image" class="w-16 h-16 object-cover rounded-md mb-2 border-4 border-gray-400" />
                {{ album.album_name }}
              </td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                <img :src="album.artist.avatar" alt="Artist Image" class="w-16 h-16 object-cover rounded-md mb-2 border-4 border-gray-400" />
                {{ album.artist.artist_name }}
              </td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                <img :src="album.genre.genre_image" alt="Genre Image" class="w-16 h-16 object-cover rounded-md mb-2 border-4 border-gray-400" />
                {{ album.genre.genre_name }}
              </td>

              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                {{ album.number_of_tracks }}
              </td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                {{ album.album_year }}
              </td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                {{ album.studio }}
              </td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                {{ album.producer }}
              </td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                <span v-if="album.status">Active</span>
                <span v-else>Inactive</span>
              </td>
              <td class="bg-gray-200 relative whitespace-nowrap py-4 pl-3 pr-4 text-center text-l font-medium sm:pr-0">
                <RouterLink :to="`/admin/album/${album.id}`" class="text-green-800 hover:text-red-600 mr-4">View</RouterLink>|
                <RouterLink :to="`/admin/album/${album.id}/edit`" class="text-green-800 hover:text-red-600 ml-4 mr-4">Edit</RouterLink>

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

const albums = ref([]);

fetch('https://2xo55fszd9.execute-api.ap-southeast-1.amazonaws.com/dev/albums')
    .then((response) => response.json())
    .then((response) => {
      console.log(response)
      albums.value = response.body
    })

// const albums = [
//   {
//     id: 1,
//     album_name : "Echoes of Eternity",
//     number_of_tracks : 10,
//     album_year : 2020,
//     album_description : "The description of Echoes of Eternity",
//     album_image : "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Album-Images/Echoes-of-Eternity.jpg",
//     artist : {
//       id :1,
//       artist_name : "Olivia Fontaine",
//       avatar : "IMAGE_URL",
//       birth_date : "1984-12-12",
//       country : "USA",
//       bio : "Olivia Fontaine biography"
//     },
//     studio : "Echoes Songs",
//     genre : "Pop",
//     producer : "Stevan Johns",
//     sort_order : 0,
//     status : true
//   },
//   {
//     id: 2,
//     album_name : "Midnight Serenade" ,
//     number_of_tracks : 10,
//     album_year : 2020,
//     album_description : "The description of Midnight Serenade",
//     album_image : "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Album-Images/Midnight-Serenade.jpg",
//     artist : {
//       id :2,
//       artist_name : "Sophia Beaumont",
//       avatar : "IMAGE_URL",
//       birth_date : "1983-10-22",
//       country : "USA",
//       bio : "Sophia Beaumont biography"
//     },
//     studio : "Midnight Songs",
//     genre : "Electronic",
//     producer : "Sheldon Cooper",
//     sort_order : 0,
//     status : true
//   },
//   {
//     id: 3,
//     album_name : "Whispers in the Wind",
//     number_of_tracks : 10,
//     album_year : 2021,
//     album_description : "The description of Whispers in the Wind",
//     album_image : "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Album-Images/Whispers-in-the-Wind.jpg",
//     artist : {
//       id :3,
//       artist_name : "William Montgomery",
//       avatar : "IMAGE_URL",
//       birth_date : "1980-09-02",
//       country : "USA",
//       bio : "William Montgomery biography"
//     },
//     studio : "Whispers Songs",
//     genre : "Blues",
//     producer : "Jordan Hill",
//     sort_order : 0,
//     status : true
//   },
//   {
//     id: 4,
//     album_name : "Dreamscape Chronicles",
//     number_of_tracks : 10,
//     album_year : 2021,
//     album_description : "The description of Dreamscape Chronicles",
//     album_image : "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Album-Images/Dreamscape-Chronicles.jpg",
//     artist : {
//       id :4,
//       artist_name : "Benjamin Sterling",
//       avatar : "IMAGE_URL",
//       birth_date : "1981-07-27",
//       country : "USA",
//       bio : "Benjamin Sterling biography"
//     },
//     studio : "Dreamscape Songs",
//     genre : "Techno",
//     producer : "Mike Edwards",
//     sort_order : 0,
//     status : true
//   },
//   {
//     id: 5,
//     album_name : "Soulful Symphonies",
//     number_of_tracks : 10,
//     album_year : 2022,
//     album_description : "The description of Soulful Symphonies",
//     album_image : "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Album-Images/Soulful-Symphonies.jpg",
//     artist : {
//       id :5,
//       artist_name : "Liam Sinclair",
//       avatar : "IMAGE_URL",
//       birth_date : "1988-02-02",
//       country : "USA",
//       bio : "Liam Sinclair biography"
//     },
//     studio : "Soulful Songs",
//     genre : "House",
//     producer : "Paul Jenner",
//     sort_order : 0,
//     status : true
//   },
//   {
//     id: 6,
//     album_name : "Rhythm of the Cosmos",
//     number_of_tracks : 10,
//     album_year : 2022,
//     album_description : "The description of Rhythm of the Cosmos",
//     album_image : "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Album-Images/Rhythm-of-the-Cosmos.jpg",
//     artist : {
//       id :1,
//       artist_name : "Olivia Fontaine",
//       avatar : "IMAGE_URL",
//       birth_date : "1984-12-12",
//       country : "USA",
//       bio : "Olivia Fontaine biography"
//     },
//     studio : "Rhythm Songs",
//     genre : "Pop",
//     producer : "Stevan Beverly",
//     sort_order : 0,
//     status : true
//   },
//   {
//     id: 7,
//     album_name : "Melodies of the Heart",
//     number_of_tracks : 10,
//     album_year : 2023,
//     album_description : "The description of Melodies of the Heart",
//     album_image : "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Album-Images/Melodies-of-the-Heart.jpg",
//     artist : {
//       id :2,
//       artist_name : "Sophia Beaumont",
//       avatar : "IMAGE_URL",
//       birth_date : "1983-10-22",
//       country : "USA",
//       bio : "Sophia Beaumont biography"
//     },
//     studio : "Melodies Songs",
//     genre : "Electronic",
//     producer : "Meena Patel",
//     sort_order : 0,
//     status : true
//   },
//   {
//     id: 8,
//     album_name : "Aurora Dreams",
//     number_of_tracks : 10,
//     album_year : 2023,
//     album_description : "The description of Aurora Dreams",
//     album_image : "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Album-Images/Aurora-Dreams.jpg",
//     artist : {
//       id :3,
//       artist_name : "William Montgomery",
//       avatar : "IMAGE_URL",
//       birth_date : "1980-09-02",
//       country : "USA",
//       bio : "William Montgomery biography"
//     },
//     studio : "Aurora Songs",
//     genre : "Blues",
//     producer : "Xavier Liam",
//     sort_order : 0,
//     status : true
//   },
//   {
//     id: 9,
//     album_name : "Harmony Haven",
//     number_of_tracks : 10,
//     album_year : 2024,
//     album_description : "The description of Harmony Haven",
//     album_image : "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Album-Images/Harmony-Haven.jpg",
//     artist : {
//       id :4,
//       artist_name : "Benjamin Sterling",
//       avatar : "IMAGE_URL",
//       birth_date : "1981-07-27",
//       country : "USA",
//       bio : "Benjamin Sterling biography"
//     },
//     studio : "Harmony Songs",
//     genre : "Techno",
//     producer : "Jeremy Sisto",
//     sort_order : 0,
//     status : true
//   },
//   {
//     id: 10,
//     album_name : "Journey Through Time",
//     number_of_tracks : 10,
//     album_year : 2024,
//     album_description : "The description of Journey Through Time",
//     album_image : "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Album-Images/Journey-Through-Time.jpg",
//     artist : {
//       id :5,
//       artist_name : "Liam Sinclair",
//       avatar : "IMAGE_URL",
//       birth_date : "1988-02-02",
//       country : "USA",
//       bio : "Liam Sinclair biography"
//     },
//     studio : "Journey Songs",
//     genre : "House",
//     producer : "Stephen Patel",
//     sort_order : 0,
//     status : true
//   },
// ]

</script>
<style></style>
