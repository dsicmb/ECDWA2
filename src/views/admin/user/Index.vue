<template>
  <div class="px-4 sm:px-6 lg:px-8">
    <div class="sm:flex sm:items-center">
      <div class="sm:flex-auto"></div>
      <div class="mt-4 sm:ml-16 sm:mt-0 sm:flex-none">
        <RouterLink
            to="/admin/user/create"
            type="button"
            class="block rounded-md bg-green-800  px-3 py-2 text-center text-sm font-semibold text-white shadow-sm
            hover:bg-white hover:text-green-800 hover:border-green-800
            border-2 border-green-800 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2
            focus-visible:outline-green-800">
          Add A User
        </RouterLink>
      </div>
    </div>
    <div class="mt-8 flow-root">
      <div class="-mx-4 -my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
        <div class="inline-block min-w-full py-2 align-middle sm:px-6 lg:px-8">
          <table class="min-w-full divide-y divide-gray-300">
            <thead class="bg-gray-200">
            <tr>
              <th scope="col" class="py-3.5 pl-4 pr-3 text-center text-sm font-semibold text-green-800 sm:pl-0">ID</th>
              <th scope="col" class="px-3 py-3.5 text-left text-base font-semibold text-green-800">First Name</th>
              <th scope="col" class="px-3 py-3.5 text-left text-base font-semibold text-green-800">Last Name</th>
              <th scope="col" class="px-3 py-3.5 text-left text-base font-semibold text-green-800">E-mail</th>
              <th scope="col" class="px-3 py-3.5 text-left text-base font-semibold text-green-800">Password</th>
              <th scope="col" class="px-3 py-3.5 text-left text-base font-semibold text-green-800">Age</th>
              <th scope="col" class="px-3 py-3.5 text-left text-base font-semibold text-green-800">Gender</th>
              <th scope="col" class="px-3 py-3.5 text-left text-base font-semibold text-green-800">City</th>
              <th scope="col" class="px-3 py-3.5 text-left text-base font-semibold text-green-800">Country</th>
              <th scope="col" class="px-3 py-3.5 text-left text-base font-semibold text-green-800">Subscription</th>
              <th scope="col" class="px-3 py-3.5 text-left text-base font-semibold text-green-800">Phone</th>
              <th scope="col" class="relative py-3.5 pl-3 pr-4 sm:pr-0">
                <span class="sr-only">Edit</span>
              </th>
            </tr>
            </thead>
            <tbody class="divide-y divide-gray-200">
            <tr v-for="user in users" :key="user.id">
              <td class="whitespace-nowrap py-4 pl-4 pr-3 text-center font-medium text-gray-900 sm:pl-0">
                <span class="inline-block w-8 h-8 rounded-full bg-gray-200 flex items-center justify-center">
                  {{ user.id }}</span>
              </td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">{{ user.first_name }}</td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">{{ user.last_name }}</td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">{{ user.email }}</td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">{{ user.password }}</td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">{{ user.age }}</td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">{{ user.gender }}</td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">{{ user.city }}</td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">{{ user.country }}</td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">{{ user.subscription }}</td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">{{ user.phone }}</td>
              <td class="bg-gray-200 relative whitespace-nowrap py-4 pl-3 pr-4 text-center text-l font-medium sm:pr-0">
                <RouterLink :to="`/admin/user/${user.id}`" class="text-green-800 hover:text-red-600 mr-4">View</RouterLink>|
                <RouterLink :to="`/admin/user/${user.id}/edit`" class="text-green-800 hover:text-red-600 ml-4 mr-4">Edit</RouterLink>
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

const users = ref([]);

fetch('https://2xo55fszd9.execute-api.ap-southeast-1.amazonaws.com/dev/users')
    .then((response) => response.json())
    .then((response) => {
      console.log(response)
      users.value = response.body
    })

// const users = [
//   {
//     id : 1,
//     first_name : "Johnathan",
//     last_name : "Derik",
//     email : "Johndsi11@gmail.com",
//     password : "dsi1",
//     age : 40,
//     gender : "Male",
//     city : "Kandana",
//     country : "Sri Lanka",
//     subscription : "Personal",
//     phone : "+94710905679"
//   },
//   {
//     id : 2,
//     first_name : "Stephen",
//     last_name : "Harvard",
//     email : "Hardsi2@gmail.com",
//     password : "dsi2",
//     age : 30,
//     gender : "Male",
//     city : "Katana",
//     country : "Sri Lanka",
//     subscription : "Family",
//     phone : "+94720905629"
//   },
//   {
//     id : 3,
//     first_name : "Andrea",
//     last_name : "Johns",
//     email : "Andsi3@gmail.com",
//     password : "dsi3",
//     age : 30,
//     gender : "Female",
//     city : "Kandy",
//     country : "Sri Lanka",
//     subscription : "Business",
//     phone : "+94730905649"
//   },
//   {
//     id : 4,
//     first_name : "Sheldon",
//     last_name : "Cooper",
//     email : "Shadsi4@gmail.com",
//     password : "dsi4",
//     age : 38,
//     gender : "Male",
//     city : "Kaluthara",
//     country : "Sri Lanka",
//     subscription : "Group",
//     phone : "+94750905109"
//   },
//   {
//     id : 5,
//     first_name : "Brandon",
//     last_name : "Lee",
//     email : "Baradsi1@gmail.com",
//     password : "dsi4",
//     age : 32,
//     gender : "Male",
//     city : "Kegalle",
//     country : "Sri Lanka",
//     subscription : "Personal",
//     phone : "+94714445649"
//   },
// ]
</script>
<style></style>
