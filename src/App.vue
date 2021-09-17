<template>
  <main
    class="flex flex-col  flex-1 p-8 overflow-y-auto border-b border-gray-300 h-screen bg-gray-100 border-solid"
  >
    <!-- Form Page -->
    <form action="" enctype="multipart/form-data" @submit.prevent="submitForm">
      <div class="bg-white rounded-lg shadow p-10">
        <!-- Page Header  -->
        <lord-icon
          v-if="isSaving"
          src="https://cdn.lordicon.com/lupuorrc.json"
          trigger="loop"
          colors="primary:#ee6d66,secondary:#7166ee"
          stroke="22"
          style="width:150px;height:150px"
        >
        </lord-icon>

        <h1 class="text-lg sm:text-2xl font-medium text-gray-900 ">
          Vue 3 Form Page using Vuelidate
        </h1>
        <p class="text-gray-500 mt-2 font-normal text-sm sm:text-lg">
          This is a vue form page using vuelidate and vue 3 having basic
          components!
        </p>
        <hr class="mt-3" />
        <div
          class="grid gap-6 sm:grid-col-1 my-6 sm:mt-12 sm:gap-8 md:grid-cols-2"
        >
          <!-- Select Input  -->
          <div>
            <label
              for="car_type"
              class="flex text-base font-medium text-gray-700"
            >
              Car Type
            </label>

            <select
              v-model="formData.car_type"
              id="car_type"
              name="car_type"
              class="mt-1 block  w-full pl-3 pr-10 py-2 text-base border p-1 border-gray-300 focus:outline-none sm:text-sm rounded-md"
            >
              <option>MUV</option>
              <option selected="">SUV</option>
              <option>XUV</option>
            </select>

            <span
              class="text-red-500 flex text-left text-md font-medium mt-2"
              v-if="v$.car_type.$error && v$.car_type.$errors[0].$message"
            >
              {{ v$.car_type.$errors[0].$message }}
            </span>
          </div>

          <div>
            <label
              for="car_brand"
              class="flex text-base font-medium text-gray-700"
            >
              Car Brand
            </label>

            <select
              v-model="formData.car_brand"
              id="car_brand"
              name="car_brand"
              class="mt-1 block w-full pl-3 pr-10 py-2 text-base border-gray-300 border p-1 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm rounded-md"
            >
              <option>Hundai</option>
              <option>Suzuki</option>
              <option>Skoda</option>
            </select>

            <span
              class="text-red-500 flex text-left text-md font-medium mt-2"
              v-if="v$.car_brand.$error && v$.car_brand.$errors[0].$message"
            >
              {{ v$.car_brand.$errors[0].$message }}
            </span>
          </div>

          <!-- Basic Input  -->
          <div>
            <label for="price" class="flex text-base font-medium text-gray-700">
              Price
            </label>

            <div class="mt-1">
              <input
                v-model="formData.price"
                type="text"
                name="price"
                id="price"
                class="shadow-sm focus:ring-indigo-500 focus:border-indigo-500 block w-full sm:text-sm border-gray-300 border p-2 rounded-md"
              />

              <span
                class="text-red-500 flex text-left text-md font-medium mt-2"
                v-if="v$.price.$error && v$.price.$errors[0].$message"
              >
                {{ v$.price.$errors[0].$message }}
              </span>
            </div>
          </div>
          <fieldset class="space-y-5">
            <label
              for="available_cities"
              class="flex text-base font-medium text-gray-700"
            >
              Available cities
            </label>

            <div class="relative flex items-start">
              <div class="sm:flex  text-left items-center sm:space-x-6 sm:h-2">
                <div v-for="city in cities" :key="city.name">
                  <input
                    v-model="formData.available_cities"
                    type="checkbox"
                    :value="city.name"
                    class="focus:ring-indigo-500 border h-4 w-4 text-indigo-600 border-gray-300 rounded"
                  />
                  <label
                    :for="city.name"
                    class="font-medium cursor-pointer ml-2 text-gray-700"
                  >
                    {{ city.name }}
                  </label>
                </div>
              </div>
            </div>

            <span
              class="text-red-500 flex text-left text-md font-medium"
              v-if="
                v$.available_cities.$error &&
                  v$.available_cities.$errors[0].$message
              "
            >
              {{ v$.available_cities.$errors[0].$message }}
            </span>
          </fieldset>

          <!-- Select File Uploader Component  -->

          <BaseFileUpload @change="uploadImage" />

          <!-- Radio Input -->
          <div>
            <label
              for="status"
              class="flex text-base font-medium text-gray-700"
            >
              Status
            </label>

            <div class="flex mt-2 items-center space-x-4">
              <input
                v-model="formData.status"
                type="radio"
                id="yes"
                value="true"
                class="focus:ring-indigo-500  h-4 w-4 text-indigo-600 border  border-gray-300"
              />

              <label
                for="yes"
                class="ml-3 block cursor-pointer text-sm font-medium text-gray-700"
              >
                Active
              </label>

              <div class="ml-4 flex">
                <input
                  v-model="formData.status"
                  type="radio"
                  id="yes"
                  value="false"
                  class="focus:ring-indigo-500  ml-3 h-4 w-4 text-indigo-600 border  border-gray-300"
                />
                <label
                  for="no"
                  class="ml-3 block cursor-pointer text-sm font-medium text-gray-700"
                >
                  Inactive
                </label>
              </div>
            </div>

            <span
              class="text-red-500 flex text-left text-md font-medium mt-2"
              v-if="v$.status.$error && v$.status.$errors[0].$message"
            >
              {{ v$.status.$errors[0].$message }}
            </span>
          </div>
        </div>

        <hr class="mt-3" />

        <!-- Submit form Button -->
        <div class="flex justify-end mt-6">
          <button
            type="submit"
            class="inline-flex sm:w-auto w-full justify-center items-center px-4 py-2 border border-transparent text-base font-medium rounded-md shadow-sm text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
          >
            Save
          </button>
        </div>
      </div>
    </form>

    <!-- Table Form Data's  -->
    <BaseTable v-if="formData" :data="carInfo" />
  </main>
</template>

<script setup>
import BaseTable from './components/BaseTable.vue'
import BaseFileUpload from './components/BaseFileUpload.vue'
import { reactive, ref, computed, watch } from 'vue'
import useVuelidate from '@vuelidate/core'
import { required, minLength, numeric } from '@vuelidate/validators'

// Local State

let formData = reactive({
  car_type: '',
  car_brand: '',
  price: null,
  available_cities: [],
  car_photo: '',
  status: '',
})
let carInfo = ref(null)
let data = reactive(null)

// Data Variable

let cities = reactive([
  { name: 'Berlin' },
  { name: 'Munich' },
  { name: 'Zurich' },
])

let isSaving = ref(false)

// Validation

const rules = computed(() => {
  return {
    car_type: {
      required,
    },
    car_brand: {
      required,
    },
    price: {
      required,
      minLength: ('Price must be 2 digit more.', minLength(2)),
      numeric: ('Enter numbers only', numeric),
    },
    available_cities: {
      required,
    },
    status: {
      required,
    },
  }
})

const v$ = useVuelidate(rules, formData)

const previewImage = ref('')

// Watch
watch(() => {
  carInfo.value = JSON.parse(window.localStorage.getItem('carInfo'))
  console.log(carInfo.value, 'as')
})

// Method

function uploadImage(event) {
  const input = event.target
  if (input.files) {
    let reader = new FileReader()
    reader.onload = (e) => {
      previewImage.value = e.target.result
      formData.car_photo = e.target.result
    }
    formData.car_photo = input.files[0]
    reader.readAsDataURL(input.files[0])
  }
}

function submitForm() {
  v$.value.$touch()
  if (v$.value.$invalid) {
    return true
  }
  data = {
    ...formData,
  }

  if (data) {
    alert('Form Submit Successfully!')
  }

  window.localStorage.setItem('carInfo', JSON.stringify(data))
  isSaving.value = true
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
