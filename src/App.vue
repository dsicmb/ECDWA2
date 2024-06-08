<template>
  <header class="bg-white">
    <nav
        class="mx-auto flex max-w-7xl items-center justify-between p-6 lg:px-8"
        aria-label="Global">
      <div class="flex lg:flex-1 items-center">
        <RouterLink to="/" class="-m-1.5 p-1.5">
          <span class="sr-only">Home</span>
          <logoStreamDreamer class="h-40 w-auto ml-10" />
        </RouterLink>



        <div class="flex flex-col ml-4"> <!-- Changed to flex-col for vertical layout -->
          <RouterLink
              to="/"
              type="button"
              class="home-button mr-6 mb-4"
              style="padding: 0.5rem 1rem; border: 2px solid transparent; border-radius: 0.5rem; text-decoration: none; transition: all 0.3s ease; background-color: #16342CFC; color: white; border-color: #16342CFC;"> <!-- Added mb-4 and mr-4 for spacing -->
            <span class="sr-only">Home</span>
            Home
          </RouterLink>

          <RouterLink
              to="/admin/album"
              type="button"
              class="admin-button mr-6"
              style="padding: 0.5rem 1rem; border: 2px solid transparent; border-radius: 0.5rem; text-decoration: none; transition: all 0.3s ease; background-color: #16342CFC; color: white; border-color: #16342CFC;"> <!-- Added mb-4 and mr-4 for spacing -->
            <!-- Added mr-4 for spacing -->
            <span class="sr-only">Admin</span>
            Admin
          </RouterLink>
        </div>




        <span v-if="showDreamStreamer" class="text-3xl font-bold ml-2" style="color: darkgreen; font-size: 90px; text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);">
          <span style="color: black;">D</span>ream<span style="color: black;">S</span>treamer
        </span>
      </div>
      <div class="flex lg:hidden">
        <button
            type="button"
            class="-m-2.5 inline-flex items-center justify-center rounded-md p-2.5 text-gray-700"
            @click="mobileMenuOpen = true">
          <span class="sr-only">Open main menu</span>
          <Bars3Icon class="h-6 w-6" aria-hidden="true" />
        </button>
      </div>

      <PopoverGroup class="hidden lg:flex lg:gap-x-12" v-if="!isHome">
        <RouterLink to="/admin/album" class="text-xl font-semibold leading-6 text-gray-400 hover:text-green-800">Albums</RouterLink>
        <RouterLink to="/admin/artist" class="text-xl font-semibold leading-6 text-gray-400 hover:text-green-800">Artists</RouterLink>
        <RouterLink to="/admin/genre" class="text-xl font-semibold leading-6 text-gray-400 hover:text-green-800">Genres</RouterLink>
        <RouterLink to="/admin/track" class="text-xl font-semibold leading-6 text-gray-400 hover:text-green-800">Tracks</RouterLink>
        <RouterLink to="/admin/user" class="text-xl font-semibold leading-6 text-gray-400 hover:text-green-800">Users</RouterLink>
      </PopoverGroup>

      <div class="hidden lg:flex lg:flex-1 lg:justify-end lg:gap-x-6">
        <a href="#" class="text-xl font-semibold leading-6 text-gray-400 hover:text-green-800">Sign up</a>
        <a href="#" class="text-xl font-semibold leading-6 text-gray-400 hover:text-green-800">Log in </a>
      </div>
    </nav>
  </header>

  <main>
    <RouterView />
  </main>

  <footer></footer>
</template>

<script setup>
import { RouterLink, RouterView, useRoute } from 'vue-router'
import { ref, computed } from 'vue'
import logoStreamDreamer from './components/icons/logoStreamDreamer.vue'

import {
  PopoverGroup,
} from '@headlessui/vue'
import {
  Bars3Icon,
} from '@heroicons/vue/24/outline'

const mobileMenuOpen = ref(false)
const route = useRoute()
const isHome = computed(() => route.path === '/')
const showDreamStreamer = computed(() => isHome.value)
</script>

<style scoped>

header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
