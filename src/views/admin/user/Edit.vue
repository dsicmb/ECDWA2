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
              <form v-on:submit.prevent="saveUser">
                <div>
                  <div class="mt-3 sm:mt-5">
                    <DialogTitle as="h1" class="text-center text-2xl font-semibold leading-6 text-green-800">
                      {{ user.first_name }} {{ user.last_name }}
                    </DialogTitle>
                    <div class="mt-4">
                      <div class="grid max-w-2xl grid-cols-1 gap-x-6 gap-y-4 sm:grid-cols-6">

                        <!-------------------------------- First Name ---------------------------------->

                        <div class="sm:col-span-3">
                          <label
                              for="first_name"
                              class="block text-sm font-medium leading-6 text-gray-900">
                            First Name
                          </label>
                          <div class="mt-2">
                            <div
                                class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2
                                focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <input
                                  type="text"
                                  name="first_name"
                                  id="first_name"
                                  class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                  v-model="user.first_name"
                              />
                            </div>
                          </div>
                        </div>

                        <!-------------------------------- Last Name ---------------------------------->

                        <div class="sm:col-span-4">
                          <label
                              for="last_name"
                              class="block text-sm font-medium leading-6 text-gray-900">
                            Last Name
                          </label>
                          <div class="mt-2">
                            <div
                                class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2
                                focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <input
                                  type="text"
                                  name="last_name"
                                  id="last_name"
                                  class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                  v-model="user.last_name"
                              />
                            </div>
                          </div>
                        </div>

                        <!-------------------------------- User Image---------------------------------->

                        <div class="sm:col-span-8">
                          <label
                              for="file"
                              class="block text-sm font-medium leading-6 text-gray-900">
                            User Image
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

                        <!-------------------------------- Email ---------------------------------->

                        <div class="sm:col-span-8">
                          <label
                              for="email"
                              class="block text-sm font-medium leading-6 text-gray-900">
                            E mail
                          </label>
                          <div class="mt-2">
                            <div
                                class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2
                                focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <input
                                  type="text"
                                  name="email"
                                  id="email"
                                  class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900
                                  placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                  v-model="user.email"/>
                            </div>
                          </div>
                        </div>

                        <!-------------------------------- Password ---------------------------------->

                        <div class="sm:col-span-8">
                          <label
                              for="password"
                              class="block text-sm font-medium leading-6 text-gray-900">
                            Password
                          </label>
                          <div class="mt-2">
                            <div
                                class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2
                                focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <input
                                  type="text"
                                  name="password"
                                  id="password"
                                  class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900
                                  placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                  v-model="user.password"/>
                            </div>
                          </div>
                        </div>

                        <!-------------------------------- Age ---------------------------------->

                        <div class="sm:col-span-4">
                          <label for="age" class="block text-sm font-medium leading-6 text-gray-900">
                            Age
                          </label>
                          <div class="mt-2">
                            <div class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2
                                        focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <select name="age" id="age" v-model="user.age"
                                      class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900
                                              placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6">
                                <option value="">Select Age</option>
                                <!-- Loop through the age range from 10 to 70 -->
                                <option v-for="age in 70" :key="age" :value="age + 10">{{ age + 10 }}</option>
                              </select>
                            </div>
                          </div>
                        </div>

                        <!-------------------------------- Gender ---------------------------------->

                        <div class="sm:col-span-3">
                          <label for="gender" class="block text-sm font-medium leading-6 text-gray-900">
                            Gender
                          </label>
                          <div class="mt-2">
                            <div class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2
                                        focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <select name="gender" id="gender" v-model="user.gender"
                                      class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900
                                             placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6">
                                <option value="">Select Gender</option>
                                <option value="Male">Male</option>
                                <option value="Female">Female</option>
                                <option value="Other">Other</option>
                              </select>
                            </div>
                          </div>
                        </div>


                        <!-------------------------------- City ---------------------------------->

                        <div class="sm:col-span-3">
                          <label
                              for="city"
                              class="block text-sm font-medium leading-6 text-gray-900">
                            City
                          </label>
                          <div class="mt-2">
                            <div
                                class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2
                                focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <input
                                  type="text"
                                  name="city"
                                  id="city"
                                  class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900
                                  placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                  v-model="user.city"/>
                            </div>
                          </div>
                        </div>

                        <!-------------------------------- Country ---------------------------------->

                        <div class="sm:col-span-4">
                          <label for="country" class="block text-sm font-medium leading-6 text-gray-900">
                            Country
                          </label>
                          <div class="mt-2">
                            <div class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2
                                         focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <select name="country" id="country" v-model="user.country"
                                      class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900
                                              placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6">
                                <option value="">Select Country</option>
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


                        <!-------------------------------- Subscription ---------------------------------->

                        <div class="sm:col-span-3">
                          <label for="subscription" class="block text-sm font-medium leading-6 text-gray-900">
                            Subscription
                          </label>
                          <div class="mt-2">
                            <div class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2
                                        focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <select name="subscription" id="subscription" v-model="user.subscription"
                                      class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900
                                             placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6">
                                <option value="">Select Subscription</option>
                                <option value="Personal">Personal</option>
                                <option value="Family">Family</option>
                                <option value="Group">Group</option>
                                <option value="Business">Business</option>
                              </select>
                            </div>
                          </div>
                        </div>


                        <!--------------------------------- Phone -------------------------------->

                        <div class="sm:col-span-4">
                          <label
                              for="phone"
                              class="block text-sm font-medium leading-6 text-gray-900">
                            Phone
                          </label>
                          <div class="mt-2">
                            <div class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset
                            focus-within:ring-indigo-600 sm:max-w-md">
                              <input
                                  type="text"
                                  name="phone"
                                  id="phone"
                                  class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0
                                  sm:text-sm sm:leading-6" v-model="user.phone"/>
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
                      to="/admin/user"
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

const user = ref( {
      id : 1,
      first_name : "Johnathan",
      last_name : "Derik",
      user_image : "https://raw.githubusercontent.com/dsicmb/WDOS-2-009983-Plants/main/User-Images/User1.jpg",
      email : "Johndsi11@gmail.com",
      password : "dsi1",
      age : 40,
      gender : "Male",
      city : "Kandana",
      country : "Sri Lanka",
      subscription : "Personal",
      phone : "+94710905679"
    }
)
const saveUser = () => {
  console.log(user)

  // route the user to the user list page
  router.push('/admin/user')
}
</script>
