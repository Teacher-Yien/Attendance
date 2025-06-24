<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
// import ApplicationLogo from '@/Components/ApplicationLogo.vue';
import Dropdown from '@/Components/Dropdown.vue';
import DropdownLink from '@/Components/DropdownLink.vue';
import NavLink from '@/Components/NavLink.vue';
import { Head } from '@inertiajs/vue3';
import { ref, computed } from 'vue';

// Sample data - replace with actual props or API calls
const stats = ref({
    present: 10,
    late: 30,
    absent: 5
});

// Current active page
const activePage = ref('dashboard');

// Sample student data
const students = ref([
    { id: 1, name: 'សុខ វិចិត្រ', class: 'Grade 10A', status: 'Present' },
    { id: 2, name: 'ចន្ទ សុភា', class: 'Grade 10A', status: 'Absent' },
    { id: 3, name: 'ពិរុណ សុវណ្ណ', class: 'Grade 10B', status: 'Late' },
    { id: 4, name: 'សុវណ្ណ មករា', class: 'Grade 10B', status: 'Present' },
    { id: 5, name: 'រដ្ឋា កញ្ញា', class: 'Grade 11A', status: 'Present' }
]);

// Navigation links
const navigationLinks = [
    {
        name: 'ទំព័រដើម',
        key: 'dashboard',
        icon: 'dashboard'
    },
    {
        name: 'និស្សិត',
        key: 'students',
        icon: 'students'
    },
    {
        name: 'របាយការណ៍',
        key: 'reports',
        icon: 'reports'
    }
];

// Function to change active page
const setActivePage = (pageKey) => {
    activePage.value = pageKey;
};

// Helper function to check if page is active
const isActivePage = (pageKey) => {
    return activePage.value === pageKey;
};
</script>

<template>
    <Head title="Dashboard" />

    <AuthenticatedLayout>
        <div class="flex min-h-screen bg-gray-100">
            <!-- Sidebar -->
            <div class="w-64 bg-white shadow-lg">
                <!-- Logo/Header -->
                <div class="flex items-center p-6 border-b">
                    <div class="w-12 h-12 bg-red-600 rounded-full flex items-center justify-center mr-3">
                        <img src="../assets/php.png" alt="">
                    </div>
                    <div>
                        <h1 class="text-lg font-semibold text-gray-800">
                            គ្រប់គ្រងវត្តមាន
                        </h1>
                        <p class="text-sm text-gray-600">Attendance Management System</p>
                    </div>
                </div>

                <!-- Navigation -->
                <nav class="mt-6">
                    <div class="px-6">
                        <p class="text-xs font-semibold text-gray-400 uppercase tracking-wider mb-3">
                            បញ្ជីថ្ងៃ
                        </p>
                    </div>
                    
                    <!-- Navigation Links -->
                    <template v-for="link in navigationLinks" :key="link.name">
                        <button 
                            @click="setActivePage(link.key)"
                            :class="[
                                'flex items-center px-6 py-3 w-full text-left transition-colors duration-200',
                                isActivePage(link.key) 
                                    ? 'text-gray-700 bg-gray-100 border-r-4 border-red-600' 
                                    : 'text-gray-600 hover:bg-gray-50 hover:text-gray-700'
                            ]"
                        >
                            <!-- Dashboard Icon -->
                            <svg v-if="link.icon === 'dashboard'" class="w-5 h-5 mr-3" fill="currentColor" viewBox="0 0 20 20">
                                <path d="M3 4a1 1 0 011-1h12a1 1 0 011 1v2a1 1 0 01-1 1H4a1 1 0 01-1-1V4zM3 10a1 1 0 011-1h6a1 1 0 011 1v6a1 1 0 01-1 1H4a1 1 0 01-1-1v-6zM14 9a1 1 0 00-1 1v6a1 1 0 001 1h2a1 1 0 001-1v-6a1 1 0 00-1-1h-2z"/>
                            </svg>
                            
                            <!-- Students Icon -->
                            <svg v-else-if="link.icon === 'students'" class="w-5 h-5 mr-3" fill="currentColor" viewBox="0 0 20 20">
                                <path d="M10.394 2.08a1 1 0 00-.788 0l-7 3a1 1 0 000 1.84L5.25 8.051a.999.999 0 01.356-.257l4-1.714a1 1 0 11.788 1.838L7.667 9.088l1.94.831a1 1 0 00.787 0l7-3a1 1 0 000-1.838l-7-3zM3.31 9.397L5 10.12v4.102a8.969 8.969 0 00-1.05-.174 1 1 0 01-.89-.89 11.115 11.115 0 01.25-3.762zM9.3 16.573A9.026 9.026 0 007 14.935v-3.957l1.818.78a3 3 0 002.364 0l5.508-2.361a11.026 11.026 0 01.25 3.762 1 1 0 01-.89.89 8.968 8.968 0 00-5.25 2.524 1 1 0 01-1.5 0z"/>
                            </svg>
                            
                            <!-- Reports Icon -->
                            <svg v-else-if="link.icon === 'reports'" class="w-5 h-5 mr-3" fill="currentColor" viewBox="0 0 20 20">
                                <path d="M9 2a1 1 0 000 2h2a1 1 0 100-2H9z"/>
                                <path fill-rule="evenodd" d="M4 5a2 2 0 012-2v1a1 1 0 102 0V3a2 2 0 012 2v6a2 2 0 01-2 2H6a2 2 0 01-2-2V5zm3 2a1 1 0 000 2h.01a1 1 0 100-2H7zm3 0a1 1 0 000 2h3a1 1 0 100-2h-3zm-3 4a1 1 0 100 2h.01a1 1 0 100-2H7zm3 0a1 1 0 100 2h3a1 1 0 100-2h-3z" clip-rule="evenodd"/>
                            </svg>
                            
                            {{ link.name }}
                        </button>
                    </template>
                </nav>
            </div>

            <!-- Main Content -->
            <div class="flex-1">
                <!-- Top Header -->
                <header class="bg-white shadow-sm border-b px-6 py-4">
                    <div class="flex items-center justify-between">
                        <h1 class="text-2xl font-semibold text-gray-800">
                            <span v-if="activePage === 'dashboard'">Dashboard</span>
                            <span v-else-if="activePage === 'students'">និស្សិត (Students)</span>
                            <span v-else-if="activePage === 'reports'">របាយការណ៍ (Reports)</span>
                        </h1>
                        <div class="flex items-center ">
                            <!-- User Avatar -->
                            <div class="  rounded-full">
                                <div class="hidden sm:ms-6 sm:flex sm:items-center">
                             <!-- Settings Dropdown  -->
                                    <div class="relative ms-3">
                                        <Dropdown align="right" width="48">
                                            <template #trigger>
                                                <span class="inline-flex rounded-md">
                                                    <button
                                                        type="button"
                                                        class="inline-flex items-center rounded-md border border-transparent bg-white px-3 py-2 text-sm font-medium leading-4 text-gray-500 transition duration-150 ease-in-out hover:text-gray-700 focus:outline-none"
                                                    >
                                                        {{ $page.props.auth.user.name }}

                                                        <svg
                                                            class="-me-0.5 ms-2 h-4 w-4"
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
                                                <DropdownLink
                                                    :href="route('profile.edit')"
                                                >
                                                    Profile
                                                </DropdownLink>
                                                <DropdownLink
                                                    :href="route('logout')"
                                                    method="post"
                                                    as="button"
                                                >
                                                    Log Out
                                                </DropdownLink>
                                            </template>
                                        </Dropdown>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </header>

                <!-- Dashboard Content -->
                <main class="p-6">
                    <!-- Stats Cards -->
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-8">
                        <!-- Present Card -->
                        <div class="bg-white rounded-lg shadow-md p-6">
                            <div class="text-center">
                                <h3 class="text-lg font-medium text-gray-600 mb-2">
                                    ចំនួនមកវត្តមាន
                                </h3>
                                <div class="text-4xl font-bold text-gray-800 mb-1">
                                    {{ stats.present }}
                                </div>
                            </div>
                        </div>

                        <!-- Late Card -->
                        <div class="bg-white rounded-lg shadow-md p-6">
                            <div class="text-center">
                                <h3 class="text-lg font-medium text-gray-600 mb-2">
                                    ចំនួនមកយឺត
                                </h3>
                                <div class="text-4xl font-bold text-orange-500 mb-1">
                                    {{ stats.late }}
                                </div>
                            </div>
                        </div>

                        <!-- Absent Card -->
                        <div class="bg-white rounded-lg shadow-md p-6">
                            <div class="text-center">
                                <h3 class="text-lg font-medium text-gray-600 mb-2">
                                    ចំនួនអវត្តមាន
                                </h3>
                                <div class="text-4xl font-bold text-red-500 mb-1">
                                    {{ stats.absent }}
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- Additional Content Area -->
                    <div class="bg-white rounded-lg shadow-md p-6">
                        <h2 class="text-xl font-semibold text-gray-800 mb-4">
                            Recent Activity
                        </h2>
                        <div class="text-gray-600">
                            <p>Additional dashboard content can be added here...</p>
                        </div>
                    </div>
                </main>
            </div>
        </div>
    </AuthenticatedLayout>
</template>