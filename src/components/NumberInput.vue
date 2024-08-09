<script setup>
import { reactive, ref } from 'vue';

const countries = reactive([
  {
    short: 'IR (+98)',
    name: "Iran (+98)"
  },
  {
    short: 'US (+1)',
    name: "United States (+1)"
  },
  {
    short: 'UK (+44)',
    name: "United Kingdom (+44)"
  },
  {
    short: 'AU (+61)',
    name: "Australia (+61)"
  },
])
const dropdownToggle = ref(false)
const selectedCountry = ref('IR (+98)')
const phoneNumber = defineModel()
</script>
<template>
  <form class="max-w-sm mx-auto">
    <div class="flex items-center">
      <button id="dropdown-phone-button" data-dropdown-toggle="dropdown-phone"
        class="flex-shrink-0 z-10 inline-flex items-center py-2.5 px-4 text-sm font-medium text-center text-gray-900 bg-white border border-gray-300 rounded-s-full dark:text-white dark:border-gray-600 focus:ring-gray-500 focus:border-gray-500"
        type="button" @click="dropdownToggle = !dropdownToggle
          ">
        {{ selectedCountry }}
        <svg class="w-2.5 h-2.5 ms-2.5" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none"
          viewBox="0 0 10 6">
          <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
            d="m1 1 4 4 4-4" />
        </svg>
      </button>
      <div id="dropdown-phone" class="z-10 bg-white divide-y divide-gray-100 rounded-lg shadow w-52 dark:bg-gray-700"
        v-if="dropdownToggle">
        <ul class="py-2 text-sm text-gray-700 dark:text-gray-200" aria-labelledby="dropdown-phone-button">
          <li v-for="(country, index) in countries" :key="index">
            <button type="button"
              class="inline-flex w-full px-4 py-2 text-sm text-gray-700 hover:bg-gray-100 dark:text-gray-200 dark:hover:bg-gray-600 dark:hover:text-white"
              role="menuitem" @click="selectedCountry = country.short">
              <span class="inline-flex items-center">
                {{ country.name }}
              </span>
            </button>
          </li>
        </ul>
      </div>
      <label for="phone-input" class="mb-2 text-sm font-medium text-gray-900 sr-only dark:text-white">Phone
        number:</label>
      <div class="relative w-full">
        <input type="text" id="phone-input"
          class="block p-2.5 w-full z-20 text-sm text-gray-900 bg-white rounded-e-full border-s-0 border border-gray-300 focus:ring-gray-500 focus:border-gray-500 outline-none dark:bg-gray-700 dark:border-s-gray-700  dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:border-blue-500"
          pattern="[0-9]{3}-[0-9]{3}-[0-9]{4}" placeholder="123-456-7890" required v-model="phoneNumber" />
      </div>
    </div>
  </form>
</template>
