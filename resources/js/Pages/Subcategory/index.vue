<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head } from '@inertiajs/vue3';
import { useForm, usePage } from '@inertiajs/vue3';
import axios from 'axios';
import { onMounted, ref } from 'vue';

const props = defineProps({
    categories: Array,
})

const page = usePage();

const subCategories = ref([]);

axios.defaults.baseURL = page.props.appUrl; 
// const BASE_URL = axios.defaults.baseURL;
const getSubCategories = (ev) => {
    // console.log('fetch sub-categories for ' + ev.target.value);
    try {
        axios.get(`/api/${ev.target.value}/sub-categories`)
            .then((response) => {
                // console.log(response.data);
                subCategories.value = response.data;
            })
    } catch (e) {
        console.log(e);
    }
}

</script>

<template>
    <Head title="Subcategory" />

    <AuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">Subcategory</h2>
        </template>

        <div>
            <div class="flex items-start space-x-9 px-44 mt-10">

            <div class="max-w-[350px] w-full p-4 bg-white border border-gray-200 rounded-lg shadow sm:p-6 md:p-8 dark:bg-gray-800 dark:border-gray-700">
                <form class="space-y-6" action="#">
                    <h5 class="text-xl font-medium text-gray-900 dark:text-white">Create Subcategory</h5>

                    <div class="m:col-span-1">
                            <label for="category" class="block text-sm font-medium leading-6 text-gray-900">Category</label>
                            <div class="mt-2">
                              <select @change="getSubCategories($event)" id="category" name="category" autocomplete="category" class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:max-w-xs sm:text-sm sm:leading-6">
                                <option selected disabled   >Select Category</option>
                                <option v-for="cat in categories" :key="cat.id" :value="cat.id">{{ cat.catname }}</option>
                              </select>
                              <div class="text-sm text-red-500 italic"></div>
                            </div>
                          </div>

                    <div>
                        <label for="subcatname" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Subcategory Name: </label>
                        <input type="text" name="subcatname" id="subcatname" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white" placeholder="Subcategory Name" required>
                    </div>


                    <button type="submit" class="w-full text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">Add Subcategory</button>
                </form>
            </div>


                <div class="relative overflow-x-auto shadow-md sm:rounded-lg w-full">
                    <table class="w-full text-sm text-left rtl:text-right text-gray-500 dark:text-gray-400">
                        <thead class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
                            <tr>
                                <th scope="col" class="px-6 py-3">
                                   #
                                </th>
                                <th scope="col" class="px-6 py-3">
                                    Subcategory Name
                                </th>
                                <th scope="col" class="px-6 py-3">
                                    Action
                                </th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="subcategory in subCategories" :key="subcategory.id" class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                                <th scope="row" class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                                    {{ subcategory.id }}
                                </th>

                                <td class="px-6 py-4">
                                    {{ subcategory.subcatname }}
                                </td>
                                <td class="px-6 py-4">
                                    <a href="#" class="font-medium text-blue-600 dark:text-blue-500 hover:underline">Edit</a>
                                </td>
                            </tr>

                        </tbody>
                    </table>
                </div>

        </div>
    </div>
    </AuthenticatedLayout>
</template>
