<script setup>
import TextInput from '@/Components/TextInput.vue';
import InputError from '@/Components/InputError.vue';
import { useForm, usePage } from '@inertiajs/vue3';
import { onMounted } from 'vue';
import axios from 'axios';

const props = defineProps({
    category: Object,
})

const page = usePage();

axios.defaults.baseURL = page.props.appUrl;

onMounted(() => {
    try {
        axios.get(`/api/categories/${props.category.id}/subcategories`)
        .then((response) => {
            console.log(response.data);
        })
    } catch (error) {
        console.log(error)
    }
})
</script>

<template></template>
