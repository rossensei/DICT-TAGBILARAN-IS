<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import TextInput from '@/Components/TextInput.vue';
import InputLabel from '@/Components/InputLabel.vue';
import InputError from '@/Components/InputError.vue';
import CategoryItem from './CategoryItem.vue';
import { Head, useForm } from '@inertiajs/vue3';

const props = defineProps({
    categories: Array
})

const form = useForm({
    catname: '',
})

const submit = () => {
    form.post('/categories/new-category', {
        onSuccess: () => form.reset()
    });
}
</script>

<template>
    <Head title="Categories" />

    <AuthenticatedLayout>
        <template #header>
            <h1 class="text-2xl font-semibold text-gray-700">Categories</h1>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <p class="text-gray-900 mb-4">Add categories, then associate items to them from items page. You can add categories and subcategories as many as you like.</p>
                <div class="p-4 bg-white shadow-sm w-[600px] rounded-lg border-l-8 border-blue-700 mb-4">
                    <form class="flex items-center space-x-2" @submit.prevent="submit">
                        <div class="flex-1 relative">
                            <TextInput 
                            v-model="form.catname" 
                            id="catname" 
                            class="w-full text-sm rounded-md"
                            :class="{ 'border-red-600' : form.errors.catname }"
                            />

                            <button 
                            v-if="form.catname !== null && form.catname !== ''" 
                            type="button" 
                            @click="form.reset()"
                            class="absolute right-0 top-1/2 botton-1/2 transform -translate-x-1/2 -translate-y-1/2 text-gray-500 hover:text-gray-600">
                            <i class="fa-solid fa-rotate-left"></i>
                            </button>
                        </div>
    
                        <button type="submit" class="text-sm text-white bg-blue-700 hover:bg-blue-600 px-4 py-2 rounded-md" :disabled="form.processing">
                            <i v-if="form.processing" class="fa-solid fa-spinner text-md animate-spin"></i>
                            <span v-else>Create</span>
                        </button>
                    </form>
                    <InputError :message="form.errors.catname" />
                </div>

                <div class="p-4 bg-white shadow-sm rounded-md w-[600px]">
                    <ul class="divide-y divide-gray-200">
                        <li v-for="cat in categories" :key="cat.id">
                            <CategoryItem :category="cat" />
                        </li>
                    </ul>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>