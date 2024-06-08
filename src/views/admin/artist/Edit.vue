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
          leave-to="opacity-0">
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
              <form v-on:submit.prevent="saveArtist">
                <div>
                  <div class="mt-3 sm:mt-5">
                    <DialogTitle as="h1" class="text-center text-2xl font-semibold leading-6 text-green-800">
                      {{ artist.artist_name }}
                    </DialogTitle>
                    <div class="mt-4">
                      <div class="grid max-w-2xl grid-cols-1 gap-x-6 gap-y-4 sm:grid-cols-6">
                        <div class="sm:col-span-8">
                          <label
                              for="artist_name"
                              class="block text-sm font-medium leading-6 text-gray-900">
                            Artist Name
                          </label>
                          <div class="mt-2">
                            <div
                                class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2
                                focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <input
                                  type="text"
                                  name="artist_name"
                                  id="artist_name"
                                  class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                  v-model="artist.artist_name"
                              />
                            </div>
                          </div>
                        </div>

                        <!-------------------------------- Avatar ---------------------------------->

                        <div class="sm:col-span-8">
                          <label
                              for="avatar"
                              class="block text-sm font-medium leading-6 text-gray-900">
                            Avatar
                          </label>
                          <div class="mt-2">
                            <div
                                class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2
                                focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <input
                                  type="file"
                                  name="avatar"
                                  id="avatar"
                                  class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900
                                  placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"/>
                            </div>
                          </div>
                        </div>

                        <!--------------------------------- Date of Birth -------------------------------->

                        <div class="sm:col-span-3">
                          <label for="birth_date" class="block text-sm font-medium leading-6 text-gray-900">
                            Date of Birth
                          </label>
                          <div class="mt-2">
                            <div class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <input type="date" name="birth_date" id="birth_date" class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                     v-model="artist.birth_date" />
                            </div>
                          </div>
                        </div>

                        <!------------------------- Country --------------------------->
                        <div class="sm:col-span-4">
                          <label for="country" class="block text-sm font-medium leading-6 text-gray-900">
                            Country
                          </label>
                          <div class="mt-2">
                            <div class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2
                                focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <select name="country" id="country"
                                      class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                      v-model="artist.country">
                                <option value="Australia">Australia</option>
                                <option value="Bahamas">Bahamas</option>
                                <option value="Barbados">Barbados</option>
                                <option value="Belize">Belize</option>
                                <option value="Botswana">Botswana</option>
                                <option value="Cameroon">Cameroon</option>
                                <option value="Canada">Canada</option>
                                <option value="Dominica">Dominica</option>
                                <option value="Fiji">Fiji</option>
                                <option value="Ghana">Ghana</option>
                                <option value="Grenada">Grenada</option>
                                <option value="Guyana">Guyana</option>
                                <option value="India">India</option>
                                <option value="Ireland">Ireland</option>
                                <option value="Jamaica">Jamaica</option>
                                <option value="Kenya">Kenya</option>
                                <option value="Liberia">Liberia</option>
                                <option value="Malawi">Malawi</option>
                                <option value="Malaysia">Malaysia</option>
                                <option value="Mauritius">Mauritius</option>
                                <option value="Namibia">Namibia</option>
                                <option value="New Zealand">New Zealand</option>
                                <option value="Nigeria">Nigeria</option>
                                <option value="Pakistan">Pakistan</option>
                                <option value="Papua New Guinea">Papua New Guinea</option>
                                <option value="Philippines">Philippines</option>
                                <option value="Rwanda">Rwanda</option>
                                <option value="Saint Lucia">Saint Lucia</option>
                                <option value="Sierra Leone">Sierra Leone</option>
                                <option value="Singapore">Singapore</option>
                                <option value="Solomon Islands">Solomon Islands</option>
                                <option value="South Africa">South Africa</option>
                                <option value="Sri Lanka">Sri Lanka</option>
                                <option value="Suriname">Suriname</option>
                                <option value="Tanzania">Tanzania</option>
                                <option value="Tonga">Tonga</option>
                                <option value="Trinidad and Tobago">Trinidad and Tobago</option>
                                <option value="Tuvalu">Tuvalu</option>
                                <option value="Uganda">Uganda</option>
                                <option value="UK">United Kingdom</option>
                                <option value="USA">United States</option>
                                <option value="Zimbabwe">Zimbabwe</option>
                              </select>
                            </div>
                          </div>
                        </div>

                        <!--------------------------- Bio ----------------------------->

                        <div class="sm:col-span-8">
                          <label
                              for="bio"
                              class="block text-sm font-medium leading-6 text-gray-900">
                            Bio
                          </label>
                          <div class="mt-2">
                            <div
                                class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2
                                focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <input
                                  type="text"
                                  name="bio"
                                  id="bio"
                                  class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900
                                  placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                  v-model="artist.bio" />
                            </div>
                          </div>
                        </div>

                        <!-------------------------------- Album Main Title ---------------------------------->

                        <div class="sm:col-span-8 mt-6">
                          <label
                              for="Albums"
                              class="block text-md font-medium leading-6 text-gray-900">
                            Albums
                          </label>
                        </div>



                        <!-------------------------------- Albums ---------------------------------->

                        <div class="sm:col-span-8" v-for="(album, index) in artist.albums" :key="index">
                          <div class="bg-white rounded-lg shadow-lg p-4 mb-4 border border-gray-300">
                            <label :for="'albumName' + index" class="block text-sm font-medium leading-6 text-gray-900">
                              Album Name {{ index + 1 }}
                            </label>
                            <div class="mt-2">
                              <div class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                                <input
                                    type="text"
                                    :name="'albumName' + index"
                                    :id="'albumName' + index"
                                    class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                    v-model="album.album_name"
                                />
                              </div>
                            </div>
                            <label :for="'albumImage' + index" class="block mt-4 text-sm font-medium leading-6 text-gray-900">
                              Album Image {{ index + 1 }}
                            </label>
                            <div class="mt-2">
                              <div class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                                <input
                                    type="file"
                                    :name="'albumImage' + index"
                                    :id="'albumImage' + index"
                                    class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                    accept="image/*"
                                    @change="handleFileUpload($event, index)"
                                />
                              </div>
                            </div>
                            <label :for="'albumYear' + index" class="block mt-4 text-sm font-medium leading-6 text-gray-900">
                              Album Year {{ index + 1 }}
                            </label>
                            <div class="mt-2">
                              <div class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                                <select
                                    :name="'albumYear' + index"
                                    :id="'albumYear' + index"
                                    class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                    v-model="album.album_year"
                                >
                                  <option disabled value="">Select Year</option>
                                  <!-- Dynamically populate the options using v-for -->
                                  <option v-for="year in availableYears" :key="year" :value="year">{{ year }}</option>
                                </select>
                              </div>
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
                      to="/admin/artist"
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

// Function to generate a range of years
const generateYearRange = (start, end) => {
  const years = [];
  for (let year = start; year <= end; year++) {
    years.push(year);
  }
  return years;
};

// Define the start and end years for the range
const startYear = 1970; // Change this to your desired start year
const endYear = new Date().getFullYear(); // Current year

// Generate the range of years
const availableYears = generateYearRange(startYear, endYear);

const open = ref(true)

const router = useRouter()

const artist = ref({
      artist_name : "Olivia Fontaine",
      avatar : "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Artist-Images/Olivia-Fontaine.jpg",
      birth_date : "1984-12-12",
      country : "USA",
      bio : "Olivia Fontaine biography",
      songs : [1,2,3],
      albums: [
        {
          id: 1,
          album_name: "Echoes of Eternity",
          album_year: 2020,
          album_image: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Album-Images/Echoes-of-Eternity.jpg"
        },
        {
          id: 6,
          album_name: "Rhythm of the Cosmos",
          album_year: 2022,
          album_image: "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/Album-Images/Rhythm-of-the-Cosmos.jpg"
        }
      ],
      sort_order : 0,
      status : true
    }
)
const saveArtist = () => {
  console.log(artist)

  // route the user to the artist list page
  router.push('/admin/artist')
}
</script>
