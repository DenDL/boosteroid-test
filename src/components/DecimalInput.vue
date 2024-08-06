<template>
  <div class="relative flex flex-col">
    <div class="relative">
      <input
          v-model="inputValue"
          @input="validateInput"
          @paste="handlePaste"
          type="text"
          min="0"
          step="any"
          id="inputValue"
          class="block px-2.5 pb-2.5 pt-4 w-full text-sm text-gray-900 bg-transparent rounded-lg border border-gray-300 appearance-none dark:text-white dark:border-gray-600 dark:focus:border-blue-500 focus:outline-none focus:ring-0 focus:border-blue-600 peer"
          :class="{'border-red-500 focus:border-red-600': error}"
          placeholder=" "
      />
      <label
          for="inputValue"
          class="absolute text-sm text-gray-500 dark:text-gray-400 duration-300 transform -translate-y-4 scale-75 top-2 z-10 origin-[0] bg-white dark:bg-gray-900 px-2 peer-focus:px-2 peer-focus:text-blue-600 peer-focus:dark:text-blue-500 peer-placeholder-shown:scale-100 peer-placeholder-shown:-translate-y-1/2 peer-placeholder-shown:top-1/2 peer-focus:top-2 peer-focus:scale-75 peer-focus:-translate-y-4 rtl:peer-focus:translate-x-1/4 rtl:peer-focus:left-auto start-1"
          :class="{'peer-focus:text-red-500 text-red-500': error}"

      >
        Enter a number
      </label>
    </div>
    <p v-if="error" class="text-red-500 text-sm mt-2">Invalid input. Only numbers and up to 18 decimal places are allowed.</p>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue';

const inputValue = ref<string>('');
const error = ref<boolean>(false);

const validateInput = (): void => {
  const regex = /^\d*\.?\d{0,18}$/;
  let splitArray = <String[]>String(inputValue.value).split('.');

  if (!regex.test(inputValue.value)
      || (splitArray.length > 1 && splitArray.at(-1)?.length > 18) && splitArray.at(-1).indexOf('e+') < 0) {
    error.value = true;
    inputValue.value = String(inputValue.value).slice(0, -1);
  } else {
    error.value = false;
  }
};

const handlePaste = (event: ClipboardEvent): void => {
  const clipboardData = event.clipboardData;

  event.preventDefault();

  if (clipboardData) {
    let pastedData = clipboardData.getData('text').replace(',', '.');
    const regex = /^\d*\.?\d{0,18}$/;

    if (!regex.test(pastedData) && Number(pastedData) >= 0) {
      pastedData = pastedData.split('.').map((part, index) => {
        if (index === 1) {
          return part.slice(0, 18);
        }
        return part;
      }).join('.');
      inputValue.value = pastedData;
    }

    inputValue.value = pastedData;
    validateInput();
  }
};
</script>
