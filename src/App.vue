<template>
  <main
    class="flex flex-col  flex-1 p-8 overflow-y-auto border-b border-gray-300 h-screen bg-gray-100 border-solid"
  >
    <!-- Form Page -->

    <form action="" @click="submitForm">
      <div class="bg-white rounded-lg shadow p-10">
        <!-- Page Header  -->

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
              Field is Required
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
              <option selected="">Suzuki</option>
              <option>Skoda</option>
            </select>

            <span
              class="text-red-500 flex text-left text-md font-medium mt-2"
              v-if="v$.car_brand.$error && v$.car_brand.$errors[0].$message"
            >
              Field is Required
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
                Field is Required
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
              Field is Required
            </span>
          </fieldset>

          <!-- Select File Uploader Component  -->
          <div>
            <div class="flex space-x-3 items-center">
              <label
                for="price"
                class="flex text-base font-medium text-gray-700"
              >
                Car photo
              </label>

              <span class="text-sm font-normal text-gray-500">
                (Optional)
              </span>
            </div>

            <div class="mt-2 sm:mt-0 sm:col-span-2">
              <div
                class="max-w-lg flex justify-center px-6 pt-5 pb-6 border-2 mt-2 border-gray-300 border-dashed rounded-md"
              >
                <div class="space-y-1 text-center">
                  <svg
                    class="mx-auto h-12 w-12 text-gray-400"
                    stroke="currentColor"
                    fill="none"
                    viewBox="0 0 48 48"
                    aria-hidden="true"
                  >
                    <path
                      d="M28 8H12a4 4 0 00-4 4v20m32-12v8m0 0v8a4 4 0 01-4 4H12a4 4 0 01-4-4v-4m32-4l-3.172-3.172a4 4 0 00-5.656 0L28 28M8 32l9.172-9.172a4 4 0 015.656 0L28 28m0 0l4 4m4-24h8m-4-4v8m-12 4h.02"
                      stroke-width="2"
                      stroke-linecap="round"
                      stroke-linejoin="round"
                    />
                  </svg>

                  <div class="flex text-sm text-gray-600">
                    <label
                      for="file-upload"
                      class="relative cursor-pointer bg-white rounded-md font-medium text-indigo-600 hover:text-indigo-500 focus-within:outline-none focus-within:ring-2 focus-within:ring-offset-2 focus-within:ring-indigo-500"
                    >
                      <span>Upload a file</span>
                      <input
                        type="file"
                        class="sr-only"
                        id="file-upload"
                        @change="uploadImage"
                      />
                    </label>

                    <p class="pl-1">or drag and drop</p>
                  </div>

                  <p class="text-xs text-gray-500">
                    PNG, JPG, GIF up to 10MB
                  </p>
                </div>
              </div>
            </div>
          </div>

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
                  id="no"
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
              Field is Required
            </span>
          </div>
        </div>

        <hr class="mt-3" />

        <!-- Submit form Button  -->
        <div class="flex justify-end mt-6">
          <button
            type="button"
            class="inline-flex sm:w-auto w-full justify-center items-center px-4 py-2 border border-transparent text-base font-medium rounded-md shadow-sm text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
          >
            Save
          </button>
        </div>
      </div>
    </form>

    <!-- Table Form Data's  -->

    <div v-if="formData" class="mt-10">
      <h1 class="text-lg sm:text-2xl font-medium text-gray-900 ">
        List of Data
      </h1>

      <div class="flex flex-col mt-4">
        <div class="-my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
          <div
            class="py-2 align-middle inline-block min-w-full sm:px-6 lg:px-8"
          >
            <div
              class="shadow overflow-hidden border-b border-gray-200 sm:rounded-lg"
            >
              <table class="min-w-full divide-y divide-gray-200">
                <thead class="bg-gray-50">
                  <tr>
                    <th
                      scope="col"
                      class="px-6 py-3 text-left text-xs font-bold text-gray-500 uppercase tracking-wider"
                    >
                      Car Type
                    </th>
                    <th
                      scope="col"
                      class="px-6 py-3 text-left text-xs font-bold text-gray-500 uppercase tracking-wider"
                    >
                      Car Brand
                    </th>
                    <th
                      scope="col"
                      class="px-6 py-3 text-left text-xs font-bold text-gray-500 uppercase tracking-wider"
                    >
                      Price
                    </th>
                    <th
                      scope="col"
                      class="px-6 py-3 text-left text-xs font-bold text-gray-500 uppercase tracking-wider"
                    >
                      Available Cities
                    </th>
                    <th
                      scope="col"
                      class="px-6 py-3 text-left text-xs font-bold text-gray-500 uppercase tracking-wider"
                    >
                      Car Photo
                    </th>
                    <th
                      scope="col"
                      class="px-6 py-3 text-left text-xs font-bold text-gray-500 uppercase tracking-wider"
                    >
                      Status
                    </th>
                  </tr>
                </thead>

                <tbody>
                  <tr v-if="formData" class="bg-gray-50">
                    <td
                      class="px-6 py-4 whitespace-nowrap text-left text-sm font-medium text-gray-900"
                    >
                      {{ formData.car_type }}
                    </td>
                    <td
                      class="px-6 py-4 whitespace-nowrap text-left text-sm text-gray-500"
                    >
                      {{ formData.car_brand }}
                    </td>
                    <td
                      class="px-6 py-4 whitespace-nowrap text-left text-sm text-gray-500"
                    >
                      {{ formData.price }}
                    </td>
                    <td
                      class="px-6 py-4 whitespace-nowrap text-left text-sm text-gray-500"
                    >
                      {{ formData.available_cities }}
                    </td>
                    <td
                      class="px-6 py-4 whitespace-nowrap text-left text-sm text-gray-500"
                    >
                      {{ formData.car_photo }}
                    </td>
                    <td
                      class="px-6 py-4 whitespace-nowrap text-left text-sm text-gray-500"
                    >
                      {{ formData.status ? 'Active' : 'Inactive' }}
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script setup>
import { reactive, ref, computed } from 'vue'
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

// Methods

function uploadImage(e) {
  formData.car_photo = e.target.files[0]
}

function submitForm() {
  v$.value.$touch()

  if (v$.value.$invalid) {
    return true
  }

  let data = {
    ...formData,
  }
  console.log(data)

  alert('Form Submit Successfully!')

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
