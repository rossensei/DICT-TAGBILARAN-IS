<script setup>
import TextInput from '@/Components/TextInput.vue';
// import InputLabel from '@/Components/InputLabel.vue';
import Modal from '@/Components/Modal.vue';
import InputError from '@/Components/InputError.vue';
import { router, useForm } from '@inertiajs/vue3';
import { ref } from 'vue';

const props = defineProps({
    category: Object,
})

const showSubCategories = ref(false);
const editMode = ref(false);

const form = useForm({
    catname: props.category.catname,
})

const submit = () => {
    form.patch('/categories/update-details/' + props.category.id, {
        onSuccess: () => {
            editMode.value = false;
        }
    })
}

const showModal = ref(false);

const deleteCategory = () => {
    showModal.value = true;
}

const closeModal = () => {
    showModal.value = false;
}

const confirmDelete = () => {
    router.delete(`/categories/remove/${props.category.id}`, {
        onSuccess: () => {
            closeModal()
        }
    })
}
</script>

<template>
    <div class="p-3" >
        <!-- <TextInput /> -->
        <div class="flex space-x-3" :class="{ 'items-center' : editMode }">
            <div class="shrink-0">
                <!-- show/hide subcategories button -->
                <button
                type="button"
                @click="showSubCategories = !showSubCategories"
                >
                    <i
                    class="fa-solid fa-plus transition-transform"
                    :class="{ 'rotate-45' : showSubCategories }"
                    ></i>
                </button>
            </div>
            <div class="flex-1">
                <!-- category name -->
                <span v-if="!editMode">{{ category.catname }}</span>
                <TextInput v-else v-model="form.catname" class="w-full rounded-md" />
            </div>
            <div class="shrink-0">
                <!-- action buttons -->
                <div v-if="!editMode" class="space-x-3">
                    <button type="button" @click="editMode = true"><i class="fa-solid fa-pencil"></i></button>
                    <button type="button" @click="deleteCategory"><i class="fa-solid fa-trash"></i></button>
                </div>
                <div v-else class="space-x-3">
                    <button type="button" @click.prevent="submit"><i class="fa-solid fa-check"></i></button>
                    <button type="button" @click="editMode = false"><i class="fa-solid fa-xmark"></i></button>
                </div>
            </div>
        </div>
        <InputError v-if="editMode" :message="form.errors.catname" class="ml-7" />
    </div>

    <Modal :show="showModal" maxWidth="xl" @close="closeModal">
        <div class="p-4">
            <div class="flex space-x-3 mb-3">
                <div class="shrink-0">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="w-6 h-6 text-red-600">
                    <path fill-rule="evenodd" d="M9.401 3.003c1.155-2 4.043-2 5.197 0l7.355 12.748c1.154 2-.29 4.5-2.599 4.5H4.645c-2.309 0-3.752-2.5-2.598-4.5L9.4 3.003ZM12 8.25a.75.75 0 0 1 .75.75v3.75a.75.75 0 0 1-1.5 0V9a.75.75 0 0 1 .75-.75Zm0 8.25a.75.75 0 1 0 0-1.5.75.75 0 0 0 0 1.5Z" clip-rule="evenodd" />
                    </svg>
                </div>
                <div class="flex-1">
                    <h1 class="text-lg font-semibold text-red-600">Delete Confirmation</h1>
                    <p class="font-medium">Do you want to delete "{{ props.category.catname }}"?</p>
                </div>
                <div class="shrink-0">
                    <button type="button" @click="closeModal">
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M6 18 18 6M6 6l12 12" />
                        </svg>
                    </button>
                </div>
            </div>
            <div class="flex justify-end space-x-2">
                <button type="button" @click="closeModal" class="px-4 py-2 bg-gray-500 hover:bg-gray-400 rounded-lg text-white font-medium">Cancel</button>
                <button type="button" @click="confirmDelete" class="px-4 py-2 bg-blue-600 hover:bg-blue-500 rounded-lg text-white font-medium">Confirm</button>
            </div>
        </div>
    </Modal>
</template>
