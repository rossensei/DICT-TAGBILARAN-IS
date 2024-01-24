<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { ref } from 'vue';


</script>
<template>
    <Head title = "Category" />
    <AuthenticatedLayout>
            <template #header>
                Category
            </template>

<div>
    <div class="flex items-center space-x-9 px-44 mt-10">

            <div class="max-w-[350px] w-full p-4 bg-white border border-gray-200 rounded-lg shadow sm:p-6 md:p-8 dark:bg-gray-800 dark:border-gray-700">
        <form class="space-y-6" action="#">
            <h5 class="text-xl font-medium text-gray-900 dark:text-white">Category</h5>
            <div>
                <label for="catname" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Category Name: </label>
                <input type="text" name="catname" id="catname" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white" placeholder="Category Name" required>
            </div>
        
            
            <button type="submit" class="w-full text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">Add Category</button>
        </form>
    </div>

       
                <div class="relative overflow-x-auto shadow-md sm:rounded-lg w-full">
            <table class="w-full text-sm text-left rtl:text-right text-gray-500 dark:text-gray-400">
                <thead class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
                    <tr>
                        <th scope="col" class="px-6 py-3">
                            Item Name
                        </th>
                        
                        <th scope="col" class="px-6 py-3">
                            Category
                        </th>

                        <th scope="col" class="px-6 py-3">
                            Price
                        </th>
                        <th scope="col" class="px-6 py-3">
                            Action
                        </th>
                    </tr>
                </thead>
                <tbody>
                    <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                        <th scope="row" class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                        </th>

                        <td class="px-6 py-4">

                        </td>
                        <td class="px-6 py-4">
                        
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