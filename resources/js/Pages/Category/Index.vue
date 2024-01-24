<script setup>
import TextInput from '@/Components/TextInput.vue';
import InputLabel from '@/Components/InputLabel.vue';
import InputError from '@/Components/InputError.vue';
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import Modal from '@/Components/Modal.vue';
import EditComponent from './Edit.vue';
import DeleteComponent from './Delete.vue';
import { ref } from 'vue';
import { Link, useForm, Head } from '@inertiajs/vue3';

const props = defineProps({
    categories: Array,
})

const form = useForm({
    catname: '',
});

const submit = () => {
    form.post('/categories/new-category', {
        onSuccess: () => form.reset()
    });
}

//CRUD ACTIONS LOGIC
const actionType = ref('');
const showModal = ref(false);

const closeModal = () => {
    showModal.value = false;
}

const categoryToEdit = ref({});

const categoryEdit = (category) => {
    categoryToEdit.value = category;
    actionType.value = 'edit';
    showModal.value = true;
}

const categoryToDelete = ref({});

const categoryDelete = (category) => {
    categoryToDelete.value = category;
    actionType.value = 'delete';
    showModal.value = true;
}
</script>
<template>
    <Head title="Categories" />
    <AuthenticatedLayout>
        <template #header>
            <h1 class="text-2xl font-semibold">Category</h1>
        </template>

        <div>
            <div class="flex items-start space-x-9 px-44 mt-10">

                <div class="max-w-[350px] w-full p-4 bg-white border border-gray-200 rounded-lg shadow sm:p-6 md:p-8">
                    <form class="space-y-6" @submit.prevent="submit">
                        <div>
                            <InputLabel value="Category Name" for="catname" class="text-sm font-medium text-gray-900"/>
                            <TextInput v-model="form.catname" id="catname" class="w-full text-sm" />
                            <InputError :message="form.errors.catname" />
                        </div>
                    
                        
                        <button type="submit" class="w-full text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center">Add Category</button>
                    </form>
                </div>

        
                <div class="relative overflow-x-auto shadow-md sm:rounded-lg w-full">
                    <table class="w-full text-sm text-left rtl:text-right text-gray-500 dark:text-gray-400">
                        <thead class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
                            <tr>
                                <th scope="col" class="px-6 py-3">
                                    Category Name
                                </th>
                                
                                <th scope="col" class="px-6 py-3">
                                    Date Created
                                </th>
                                <th scope="col" class="px-6 py-3">
                                    Action
                                </th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="cat in categories" :key="cat.id" class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                                <th scope="row" class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                                    {{ cat.catname }}
                                </th>
                                <td class="px-6 py-4">
                                    {{ new Date(cat.created_at).toDateString() }}
                                </td>
                                <td class="px-6 py-4">
                                    <button @click="categoryEdit(cat)" type="button" class="font-medium text-blue-600 dark:text-blue-500 hover:underline">Edit</button>
                                    <button @click="categoryDelete(cat)" type="button" class="font-medium text-red-600 dark:text-red-500 hover:underline">Delete</button>
                                </td>
                            </tr>
                        
                        </tbody>
                    </table>
                </div>

            </div>
        </div>



            
    </AuthenticatedLayout>


    <Modal :show="showModal" maxWidth="xl" @close="closeModal">
        <EditComponent v-if="actionType === 'edit'" :category="categoryToEdit" @close-modal="closeModal" />
        <DeleteComponent v-else-if="actionType === 'delete'" :category="categoryToDelete" @close-modal="closeModal" />
    </Modal>
</template>