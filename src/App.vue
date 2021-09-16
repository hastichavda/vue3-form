<template>
  <main
    class="flex flex-col flex-1 p-8 overflow-y-auto border-b border-gray-300 h-screen bg-gray-100 border-solid"
  >
    <div class="bg-white rounded-lg shadow p-10">
      <div class="grid gap-6 sm:grid-col-1 my-6 md:grid-cols-2">
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
            class="mt-1 block w-full pl-3 pr-10 py-2 text-base border p-1 border-gray-300 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm rounded-md"
          >
            <option>MUV</option>
            <option selected="">SUV</option>
            <option>XUV</option>
          </select>
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
        </div>
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
              placeholder="you@example.com"
            />
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
            <div class="flex items-center space-x-3 h-5">
              <div v-for="city in cities" :key="city.name">
                <input
                  v-model="formData.available_cities"
                  type="checkbox"
                  :value="city.name"
                  class="focus:ring-indigo-500 border h-4 w-4 text-indigo-600 border-gray-300 rounded"
                />
                <label :for="city.name" class="font-medium ml-2 text-gray-700">
                  {{ city.name }}
                </label>
              </div>
            </div>
          </div>
        </fieldset>

        <div>
          <label for="price" class="flex text-base font-medium text-gray-700">
            Car photo
          </label>
          <div class="mt-1 sm:mt-0 sm:col-span-2">
            <div
              class="max-w-lg flex justify-center px-6 pt-5 pb-6 border-2 border-gray-300 border-dashed rounded-md"
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

        <div>
          <label for="status" class="flex text-base font-medium text-gray-700">
            Status
          </label>
          <div class="flex mt-4 items-center">
            <input
              v-model="formData.status"
              type="radio"
              id="yes"
              value="true"
              class="focus:ring-indigo-500 h-4 w-4 text-indigo-600 border  border-gray-300"
            />

            <label
              for="yes"
              class="ml-3 block text-sm font-medium text-gray-700"
            >
              Active
            </label>
            <input
              v-model="formData.status"
              type="radio"
              id="no"
              value="false"
              class="focus:ring-indigo-500 ml-2 h-4 w-4 text-indigo-600 border  border-gray-300"
            />
            <label
              for="no"
              class="ml-3 block text-sm font-medium text-gray-700"
            >
              Inactive
            </label>
          </div>
        </div>
      </div>
      <div class="flex justify-end">
        <button
          type="button"
          class="inline-flex items-center px-4 py-2 border border-transparent text-base font-medium rounded-md shadow-sm text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
        >
          Save
        </button>
      </div>
    </div>

    <div v-if="formData">
      <div class="flex flex-col">
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
                      class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                    >
                      Car Type
                    </th>
                    <th
                      scope="col"
                      class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                    >
                      Car Brand
                    </th>
                    <th
                      scope="col"
                      class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                    >
                      Price
                    </th>
                    <th
                      scope="col"
                      class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                    >
                      Available Cities
                    </th>
                    <th
                      scope="col"
                      class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                    >
                      Car Photo
                    </th>
                    <th
                      scope="col"
                      class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                    >
                      Status
                    </th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-if="formData" class="bg-gray-50">
                    <td
                      class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900"
                    >
                      {{ formData.car_type }}
                    </td>
                    <td
                      class="px-6 py-4 whitespace-nowrap text-sm text-gray-500"
                    >
                      {{ formData.car_brand }}
                    </td>
                    <td
                      class="px-6 py-4 whitespace-nowrap text-sm text-gray-500"
                    >
                      {{ formData.price }}
                    </td>
                    <td
                      class="px-6 py-4 whitespace-nowrap text-sm text-gray-500"
                    >
                      {{ formData.available_cities }}
                    </td>
                    <td
                      class="px-6 py-4 whitespace-nowrap text-sm text-gray-500"
                    >
                      {{ formData.car_photo }}
                    </td>
                    <td
                      class="px-6 py-4 whitespace-nowrap text-sm text-gray-500"
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
import { reactive } from 'vue'

let formData = reactive({
  car_type: '',
  car_brand: '',
  price: '',
  available_cities: [],
  car_photo: '',
  status: '',
})

let cities = reactive([
  { name: 'Berlin' },
  { name: 'Munich' },
  { name: 'Zurich' },
])

function uploadImage(e) {
  formData.car_photo = e.target.files[0]
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
