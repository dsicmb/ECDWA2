<template>
  <div class="px-4 sm:px-6 lg:px-8">
    <div class="sm:flex sm:items-center">
      <div class="sm:flex-auto">

      </div>
      <div class="mt-4 sm:ml-16 sm:mt-0 sm:flex-none">

        <RouterLink
            to="/admin/genre/create"
            type="button"
            class="block rounded-md bg-green-800  px-3 py-2 text-center text-sm font-semibold text-white shadow-sm
            hover:bg-white hover:text-green-800 hover:border-green-800
            border-2 border-green-800 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2
            focus-visible:outline-green-800">
          Add A Genre
        </RouterLink>

      </div>
    </div>
    <div class="mt-8 flow-root" >
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
                Genre
              </th>
              <th scope="col" class="px-3 py-3.5 text-left text-base font-semibold text-green-800">
                Description
              </th>
              <th scope="col" class="px-3 py-3.5 text-left text-base font-semibold text-green-800">
                Image
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
            <tr v-for="genre in genres" :key="genre.id">

              <td class="whitespace-nowrap py-4 pl-4 pr-3 text-center font-medium text-gray-900 sm:pl-0">
                <span class="inline-block w-8 h-8 rounded-full bg-gray-200 flex items-center justify-center">
                  {{ genre.id }}</span>
              </td>

              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500 font-bold">
                {{ genre.genre_name }}
              </td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                {{ genre.genre_description }}
              </td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                <img :src="genre.genre_image" alt="Genre" class="w-16 h-16 object-cover rounded-md mb-2 border-4 border-gray-400" />
              </td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                <span v-if="genre.status">Active</span>
                <span v-else>Inactive</span>
              </td>
              <td class="bg-gray-200 relative whitespace-nowrap py-4 pl-3 pr-4 text-center text-l font-medium sm:pr-0">
                <RouterLink :to="`/admin/genre/${genre.id}`" class="text-green-800 hover:text-red-600 mr-4">View</RouterLink>|
                <RouterLink :to="`/admin/genre/${genre.id}/edit`" class="text-green-800 hover:text-red-600 ml-4 mr-4">Edit</RouterLink>

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

const genres = ref([]);

fetch('https://2xo55fszd9.execute-api.ap-southeast-1.amazonaws.com/dev/genres')
    .then((response) => response.json())
    .then((response) => {
      console.log(response)
      genres.value = response.body
    })

// const genres = [
//   {
//     id : 1,
//     genre_name: "Pop",
//     genre_description: "The description of Pop",
//     genre_image : "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Genre-Images/Pop.jpg",
//     sort_order:0,
//     status: true
//   },
//   {
//     id : 2,
//     genre_name: "Electronic",
//     genre_description: "The description of Electronic",
//     genre_image : "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Genre-Images/Electronic.jpg",
//     sort_order:0,
//     status: true
//   },
//   {
//     id : 3,
//     genre_name: "Blues",
//     genre_description: "The description of Blues",
//     genre_image : "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Genre-Images/Blues.jpg",
//     sort_order:0,
//     status: true
//   },
//   {
//     id : 4,
//     genre_name: "Techno",
//     genre_description: "The description of Techno",
//     genre_image : "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Genre-Images/Techno.jpg",
//     sort_order:0,
//     status: true
//   },
//   {
//     id : 5,
//     genre_name: "House",
//     genre_description: "The description of House",
//     genre_image : "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Genre-Images/House.jpg",
//     sort_order:0,
//     status: true
//   }
// ]
</script>
<style></style>
