<script setup>
import TextInput from '@/Components/TextInput.vue';
import InputLabel from '@/Components/InputLabel.vue';
import InputError from '@/Components/InputError.vue';
import { router } from '@inertiajs/vue3';
import { defineEmits } from 'vue';

const props = defineProps({
    category: Object
})

const emits = defineEmits(['close-modal']);

const confirm = () => {
    router.delete('/categories/remove/' + props.category.id, {
        onSuccess: () => emits('close-modal')
    });
}
</script>

<template>
    <div class="p-6">

        <div class="flex items-start space-x-3">
            <div class="shrink-0">
                <!-- <ExclamationTriangleIcon class="w-6 h-6 text-red-500" /> -->
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="w-6 h-6 text-red-500">
                    <path fill-rule="evenodd" d="M9.401 3.003c1.155-2 4.043-2 5.197 0l7.355 12.748c1.154 2-.29 4.5-2.599 4.5H4.645c-2.309 0-3.752-2.5-2.598-4.5L9.4 3.003ZM12 8.25a.75.75 0 0 1 .75.75v3.75a.75.75 0 0 1-1.5 0V9a.75.75 0 0 1 .75-.75Zm0 8.25a.75.75 0 1 0 0-1.5.75.75 0 0 0 0 1.5Z" clip-rule="evenodd" />
                </svg>

            </div>

            <div class="flex-1">
                <h1 class="text-lg font-semibold text-red-600">Delete Confirmation</h1>
                <div class="text-sm text-gray-800">
                    Are you sure you want to delete "{{ props.category.catname }}"?
                    You cannot undo this action.
                </div>
            </div>

            <div class="shrink-0">
                <button @click="emits('close-modal')">
                    <!-- <XMarkIcon class="w-6 h-6 text-gray-600" /> -->
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="w-6 h-6 text-gray-600">
                        <path fill-rule="evenodd" d="M5.47 5.47a.75.75 0 0 1 1.06 0L12 10.94l5.47-5.47a.75.75 0 1 1 1.06 1.06L13.06 12l5.47 5.47a.75.75 0 1 1-1.06 1.06L12 13.06l-5.47 5.47a.75.75 0 0 1-1.06-1.06L10.94 12 5.47 6.53a.75.75 0 0 1 0-1.06Z" clip-rule="evenodd" />
                    </svg>
                </button>
            </div>
        </div>

        <div class="mt-4 flex justify-end items-center space-x-2">
            <button class="bg-gray-100 hover:bg-gray-200 px-4 py-2 rounded-lg text-sm font-medium" @click="emits('close-modal')">Cancel</button>
            <button class="bg-red-500 hover:bg-red-600 text-white px-4 py-2 rounded-lg text-sm font-medium" @click="confirm">Confirm</button>
        </div>
    </div>
</template>