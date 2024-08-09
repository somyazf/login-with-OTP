<script setup>
import { ref, reactive } from 'vue';
import NumberInput from '@/components/NumberInput.vue';

const OTP = ref(null);
const phoneNumber = ref(null);
const codeNumbers = reactive([
  { id: 'firstNumber', number: null },
  { id: 'secondNumber', number: null },
  { id: 'thirdNumber', number: null },
  {
    id: 'fourthNumber', number: null
  }])
function getOTP() {
  if (phoneNumber.value) {
    fetch('https://jsonplaceholder.typicode.com/users')
      .then(response => {
        response.json()
        OTP.value = 4569
      })
      .then(json => console.log(json))
  }
  else {
    console.log('error')
  }
}

</script>

<template>
  <main v-if="!OTP">
    <img src="../assets/images/3763928.png" class="mx-auto pb-5" />
    <h2 class="pb-2 text-xl font-semibold">Add Your Phone Number</h2>
    <p class="pb-6 font-medium w-2/5 mx-auto">Enter your phone number in order to send you an OTP security code</p>

    <div class="px-4 py-5 mx-auto bg-white rounded-lg w-5/6">
      <NumberInput v-model="phoneNumber" />
      <div class="max-w-sm mx-auto text-left px-4">
        <p class="pt-4 pb-2 text-xs text-gray-600 font-medium">YOUR PHONE NUMBER MUST CONTAIN</p>
        <div class="flex">
          <input type="radio" name="Exactly 11 numbers" id="eleven-numbers"
            :checked="phoneNumber ? phoneNumber.toString().length === 10 : false">
          <label for="eleven-numbers" class="pl-1 text-gray-600">Exactly 11 numbers</label>
        </div>
      </div>
    </div>

    <button type="submit"
      class="max-w-sm text-white w-full bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-semibold rounded-full text-base px-5 py-3 me-2 mb-2 mt-10 mx-auto dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800"
      @click="getOTP()">Send verification code</button>
  </main>
  <main v-else class="transition-transform">
    <img src="../assets/images/3763928.png" class="mx-auto pb-5" />
    <h2 class="pb-2 text-xl font-semibold">Enter The Verification Code</h2>
    <p class="pb-6 font-medium w-2/5 mx-auto">Enter the 4 digit number that we send to {{ phoneNumber }}</p>

    <div :class="'flex justify-center mx-auto w-2/5 gap-5 inputs-wrapper'">
      <input v-for="number in codeNumbers" :key="number.id" :id="number.id" v-model="number.number" type="number" />
    </div>

    <button type="submit"
      class="max-w-sm text-white w-full bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-semibold rounded-full text-base px-5 py-3 me-2 mb-2 mt-10 mx-auto dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800">Next
      Step</button>
    <p class="pt-3 font-semibold">Didn't receive anything? <span class="font-semibold text-blue-700"
        @click="OTP = null">Resend Code</span>
    </p>
  </main>
</template>
<style scoped>
.inputs-wrapper>input {
  width: 32px;
  height: 100%;
  background-color: transparent;
  text-align: center;
  border: 0;
  border-bottom: 3px solid blue;
  padding: 0;
}

.inputs-wrapper>input:focus-visible {
  outline: none;
}

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

img {
  height: 265px;
}

span {
  cursor: pointer;
}
</style>
