<script setup>
import { Head, Link } from '@inertiajs/vue3';

defineProps({
    imageUrl: String
});
</script>

<template>
    <Head title="Welcome" />
    
    <div class="w-full min-h-screen bg-blue-700">
        <div class="relative h-[300px] flex bg-white">
                <img :src="imageUrl" alt="Logo" class="w-[390px] h-[165px]">
                <div class="h-0 w-0 border-r-[100vw] border-r-transparent border-b-[7vw] border-b-red-700 absolute bottom-0 z-10"></div>
                <div class="h-0 w-0 border-r-[100vw] border-r-transparent border-t-[15.5vw] border-t-blue-700 rotate-180 absolute bottom-0"></div>

                <div class="absolute min-h-screen w-full z-20">
                    <div class="flex items-center justify-center min-h-screen">
                        <h1 class="text-4xl font-bold text-white">DICT OF THE PEOPLE AND FOR THE PEOPLE</h1>
                    </div>
                </div>
            </div>

        </div>
</template>

<style>
.bg-dots-darker {
    background-image: url("data:image/svg+xml,%3Csvg width='30' height='30' viewBox='0 0 30 30' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M1.22676 0C1.91374 0 2.45351 0.539773 2.45351 1.22676C2.45351 1.91374 1.91374 2.45351 1.22676 2.45351C0.539773 2.45351 0 1.91374 0 1.22676C0 0.539773 0.539773 0 1.22676 0Z' fill='rgba(0,0,0,0.07)'/%3E%3C/svg%3E");
}
@media (prefers-color-scheme: dark) {
    .dark\:bg-dots-lighter {
        background-image: url("data:image/svg+xml,%3Csvg width='30' height='30' viewBox='0 0 30 30' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M1.22676 0C1.91374 0 2.45351 0.539773 2.45351 1.22676C2.45351 1.91374 1.91374 2.45351 1.22676 2.45351C0.539773 2.45351 0 1.91374 0 1.22676C0 0.539773 0.539773 0 1.22676 0Z' fill='rgba(255,255,255,0.07)'/%3E%3C/svg%3E");
    }
}

.fseparator{
    width: 0;
    height: 0;
    border-right: 100vw solid transparent;
    border-bottom: 13.9vw solid red;
    margin-top: -1.9vw;
}
.Sseparator{
    width: 0;
    height: 0;
    border-right: 100vw solid transparent;
    border-top: 13.9vw solid blue;
    margin-top: -1.9vw;
    position:  relative;
    position: absolute;
    rotate: 180deg;
}

</style>


<!-- <section class="first"> -->
