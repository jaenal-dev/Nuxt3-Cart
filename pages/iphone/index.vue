<template>
    <div class="grid grid-cols-4 gap-4 mt-10">
        <nuxt-link v-for="iphone in iphones" :key="iphone" :to="`/iphone/${iphone}`"
            class="text-center border rounded-lg shadow-lg">
            <h1>{{ iphone }}</h1>
            <div class="flex justify-center">
                <img :src="`/images/${iphone}.jpg`" width="200">
            </div>
        </nuxt-link>
    </div>
</template>

<script setup>
useHead({
    title: 'Nuxt3 - Iphones'
})

// const { data } = useFetch('/iphones')
// const iphones = data
const iphones = ['iphone-12', 'iphone-12-pro', 'iphone-13-pro', 'iphone-13-pro-max']
</script>