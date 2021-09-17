<template>
  <div v-if="data" class="mt-10">
    <h1 class="text-lg sm:text-2xl font-medium text-gray-900 ">
      List of Data
    </h1>

    <div class="flex flex-col mt-4">
      <div class="-my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
        <div class="py-2 align-middle inline-block min-w-full sm:px-6 lg:px-8">
          <div
            class="shadow overflow-hidden border-b border-gray-200 sm:rounded-lg"
          >
            <!-- Table Section  -->
            <table class="min-w-full divide-y divide-gray-200" :data="data">
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

              <!-- Table body section  -->
              <tbody>
                <tr class="bg-gray-50">
                  <td
                    class="px-6 py-4 whitespace-nowrap text-left text-sm font-medium text-gray-900"
                  >
                    {{ data.car_type }}
                  </td>
                  <td
                    class="px-6 py-4 whitespace-nowrap text-left text-sm text-gray-500"
                  >
                    {{ data.car_brand }}
                  </td>
                  <td
                    class="px-6 py-4 whitespace-nowrap text-left text-sm text-gray-500"
                  >
                    {{ data.price }}
                  </td>
                  <td
                    class="px-6 py-4 whitespace-nowrap text-left text-sm text-gray-500"
                  >
                    {{ data.available_cities }}
                  </td>
                  <td
                    class="px-6 py-4 whitespace-nowrap text-left text-sm text-gray-500"
                  >
                    <img :src="data.car_photo" alt="image" class="w-20 h-10" />
                  </td>
                  <td
                    class="px-6 py-4 whitespace-nowrap text-left text-sm text-gray-500"
                  >
                    {{ data.status ? 'Active' : 'Inactive' }}
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { defineProps } from 'vue'

const props = defineProps({
  data: {
    type: [Array, Function, Object],
    required: true,
  },
})

console.log(props)
</script>
