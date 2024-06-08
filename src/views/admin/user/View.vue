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
        <div class="flex min-h-full items-end justify-center p-4 text-center sm:items-center sm:p-0">
          <TransitionChild
              as="template"
              enter="ease-out duration-300"
              enter-from="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
              enter-to="opacity-100 translate-y-0 sm:scale-100"
              leave="ease-in duration-200"
              leave-from="opacity-100 translate-y-0 sm:scale-100"
              leave-to="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95">
            <DialogPanel class="relative transform overflow-hidden rounded-lg bg-white px-4 pb-4 pt-5 text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg sm:p-6">
              <div class="bg-gray-100 px-4 py-5 sm:px-6">
                <DialogTitle as="h1" class="text-center text-2xl font-semibold leading-6 text-green-800">
                  {{ user.first_name }} {{ user.last_name }}
                </DialogTitle>
              </div>

              <div class="container" style="display: flex; justify-content: center; align-items: center; margin: 10px 0;">
                <div class="id-card" style="width: 400px; border: 1px solid #ccc; padding: 20px; border-radius: 15px; box-shadow: 0 0 10px rgba(0,0,0,0.1); font-family: Arial, sans-serif; display: flex; align-items: center;">
                  <div class="id-card-image" style="margin-right: 20px;">
                    <img :src="user.user_image" alt="User Image" style="width: 100px; height: 100px; border-radius: 50%;" />
                  </div>
                  <div class="id-card-body" style="font-size: 14px; color: #333;">
                    <p><strong>Email:</strong> {{ user.email }}</p>
                    <p><strong>Password:</strong> {{ user.password }}</p>
                    <p><strong>Age:</strong> {{ user.age }}</p>
                    <p><strong>Gender:</strong> {{ user.gender }}</p>
                    <p><strong>City:</strong> {{ user.city }}</p>
                    <p><strong>Country:</strong> {{ user.country }}</p>
                    <p><strong>Subscription:</strong> {{ user.subscription }}</p>
                    <p><strong>Phone:</strong> {{ user.phone }}</p>
                  </div>
                </div>
              </div>

              <div class="mt-3 sm:mt-4">
                <RouterLink
                    type="button"
                    class="block rounded-md bg-green-800 px-3 py-2 text-center text-sm font-semibold text-white shadow-sm
                    hover:bg-white hover:text-green-800 hover:border-green-800 border-2 border-green-800 focus-visible:outline
                    focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-green-800"
                    to="/admin/user"
                    ref="cancelButtonRef">
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

const user =
    {
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
</script>
