<template>
    <div>
        <a href="#" @click="view('home')">Home</a>
        <a href="#" @click="view('about')">About</a>
        <a href="#" @click="view('profile')">Profile</a>
        <a href="#" @click="view('iphone')">Iphone</a>
    </div>

    <!-- <NuxtPage /> -->

    <LazyHome v-if="page === 'home'" />
    <About v-if="page === 'about'" />
    <Profile v-if="page === 'profile'" />
    <Iphone v-if="page === 'iphone'" />
</template>

<script setup>
const page = ref('home')

function view(name) {
    page.value = name
}
</script>
