<script setup>
import TextInput from '@/Components/TextInput.vue';
// import InputLabel from '@/Components/InputLabel.vue';
import InputError from '@/Components/InputError.vue';
import { useForm } from '@inertiajs/vue3';
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
                    <button type="button"><i class="fa-solid fa-trash"></i></button>
                </div>
                <div v-else class="space-x-3">
                    <button type="button" @click.prevent="submit"><i class="fa-solid fa-check"></i></button>
                    <button type="button" @click="editMode = false"><i class="fa-solid fa-xmark"></i></button>
                </div>
            </div>
        </div>
        <InputError v-if="editMode" :message="form.errors.catname" class="ml-7" />
    </div>
</template>
