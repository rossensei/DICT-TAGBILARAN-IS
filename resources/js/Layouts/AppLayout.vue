<script setup>
import { ref, onMounted } from 'vue';
import Dropdown from '@/Components/Dropdown.vue';
import DropdownLink from '@/Components/DropdownLink.vue';
import NavLink from '@/Components/NavLink.vue';
import ResponsiveNavLink from '@/Components/ResponsiveNavLink.vue';
import { Link, useRemember } from '@inertiajs/vue3';

const showingNavigationDropdown = ref(false);

let isCollapsed = ref(localStorage.getItem("isCollapsed") === "true");

// onMounted(() => {
//     console.log(isCollapsed.value);
// })

const collapseSidebar = () => {
    
    isCollapsed.value = !isCollapsed.value;
    localStorage.setItem("isCollapsed", isCollapsed.value);

    // console.log(isCollapsed.value);
}

const clearLocalStorage = () => {
    localStorage.clear();
}

</script>

<template>
    <div>
        <!-- <div class="sticky top-0 h-22 w-full bg-green-300"> blah blah</div> -->
        <div class="flex items-start min-h-screen">
            <nav class="sticky top-0 z-10 bg-blue-700 min-h-screen duration-300" :class="[ !isCollapsed ? 'w-64' : 'w-16' ]">
                <div class="relative p-4">
                    <div class="flex" :class="[ !isCollapsed ? 'justify-between items-center' : 'justify-center']">
                        <!-- Logo branding -->
                        <Link :href="route('dashboard')" class="w-full flex items-center space-x-2">
                            <img src="../../../public/images/DICT-BANNER-LOGO.png" alt="mdc-logo" class="w-full mt-3">
                            <!-- <h1 v-show="!isCollapsed" class="text-md text-white font-extrabold text-center">MDC-IMS</h1> -->
                        </Link>
    
                    </div>
                    <span class="absolute -right-5 top-5 bg-gray-100 hover:bg-gray-200 text-gray-600 rounded-full p-1.5 text-center text-sm cursor-pointer peer" @click="collapseSidebar">
                          <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-[15px] h-[15px] duration-75" :class="[ isCollapsed ? 'rotate-180 peer-hover:translate-x-2' : 'rotate-0 peer-hover:-translate-x-2']">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M18.75 19.5l-7.5-7.5 7.5-7.5m-6 15L5.25 12l7.5-7.5" />
                          </svg>                     
                    </span> 
    
                    <hr v-show="!isCollapsed" class="mb-4 mt-4 bg-gray-600">
    
                    <span class="text-[10px] mb-2 text-gray-200 select-none font-bold uppercase" :class="[ isCollapsed ? 'mt-24 text-center' : '']">Menu</span>
                    <ul class="space-y-2 font-medium" :class="[ isCollapsed ? 'flex flex-col' : '']">
                        <li>
                            <NavLink :href="route('dashboard')" :active="route().current('dashboard')" class="flex items-center text-white">
                                <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" fill="currentColor" class="bi bi-speedometer2" viewBox="0 0 16 16">
                                    <path d="M8 4a.5.5 0 0 1 .5.5V6a.5.5 0 0 1-1 0V4.5A.5.5 0 0 1 8 4zM3.732 5.732a.5.5 0 0 1 .707 0l.915.914a.5.5 0 1 1-.708.708l-.914-.915a.5.5 0 0 1 0-.707zM2 10a.5.5 0 0 1 .5-.5h1.586a.5.5 0 0 1 0 1H2.5A.5.5 0 0 1 2 10zm9.5 0a.5.5 0 0 1 .5-.5h1.5a.5.5 0 0 1 0 1H12a.5.5 0 0 1-.5-.5zm.754-4.246a.389.389 0 0 0-.527-.02L7.547 9.31a.91.91 0 1 0 1.302 1.258l3.434-4.297a.389.389 0 0 0-.029-.518z"/>
                                    <path fill-rule="evenodd" d="M0 10a8 8 0 1 1 15.547 2.661c-.442 1.253-1.845 1.602-2.932 1.25C11.309 13.488 9.475 13 8 13c-1.474 0-3.31.488-4.615.911-1.087.352-2.49.003-2.932-1.25A7.988 7.988 0 0 1 0 10zm8-7a7 7 0 0 0-6.603 9.329c.203.575.923.876 1.68.63C4.397 12.533 6.358 12 8 12s3.604.532 4.923.96c.757.245 1.477-.056 1.68-.631A7 7 0 0 0 8 3z"/>
                                    </svg>
                                <span class="ml-3" v-show="!isCollapsed">Dashboard</span>
                            </NavLink>
                        </li>
                        <li>
                            <NavLink :href="route('category.index')" :active="route().current('category.index')" class="flex items-center text-white">
                                <svg class="w-6 h-6 text-white-800 dark:text-white" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
                                    <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15.6 8.4h0m-4.7 11.3-6.6-6.6a1 1 0 0 1 0-1.4l7.3-7.4a1 1 0 0 1 .7-.3H18a2 2 0 0 1 2 2v5.5a1 1 0 0 1-.3.7l-7.5 7.5a1 1 0 0 1-1.3 0Z"/>
                                </svg>
                                <span class="ml-3" v-show="!isCollapsed">Categories</span>
                            </NavLink>
                        </li>
                    </ul>
                </div>
            </nav>
            <div class="flex-1 min-h-screen overflow-hidden">
                <div class="w-full p-4 bg-white border-b border-gray-50">
                    <div class="flex justify-end">
                        <div class="ml-3 relative">
                            <Dropdown align="right" width="48">
                                <template #trigger>
                                    <span class="inline-flex rounded-md">
                                        <button
                                            type="button"
                                            class="inline-flex items-center px-3 py-2 border border-transparent text-sm leading-4 font-medium rounded-md text-gray-500 bg-white hover:text-gray-700 focus:outline-none transition ease-in-out duration-150"
                                        >
                                            {{ $page.props.auth.user.name }}

                                            <svg
                                                class="ml-2 -mr-0.5 h-4 w-4"
                                                xmlns="http://www.w3.org/2000/svg"
                                                viewBox="0 0 20 20"
                                                fill="currentColor"
                                            >
                                                <path
                                                    fill-rule="evenodd"
                                                    d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z"
                                                    clip-rule="evenodd"
                                                />
                                            </svg>
                                        </button>
                                    </span>
                                </template>

                                <template #content>
                                    <DropdownLink :href="route('profile.edit')"> Profile </DropdownLink>
                                    <DropdownLink :href="route('logout')" method="post" as="button" @click="clearLocalStorage">
                                        Log Out
                                    </DropdownLink>
                                </template>
                            </Dropdown>
                        </div>
                    </div>
                    
                </div>
                <header class="" v-if="$slots.header">
                    <div class="max-w-7xl mx-auto py-6 px-4 sm:px-6 lg:px-8">
                        <slot name="header" />
                    </div>
                </header>
                <main>
                    <slot />
                </main>
            </div>
        </div>
    </div>
</template>

<style scoped>
.slide-enter-active {
    transition: all 0.1s ease-out;
}

.slide-leave-active {
    transition: all 0.1s ease-in;
}

.slide-enter-from,
.slide-leave-to {
    transform: translateY(-20px);
}
</style>