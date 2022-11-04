<template>
    <div class="flex w-full h-screen">
        <div class="m-auto">
            <section class="h-screen">
                <div class="container h-full px-6 py-12">
                    <div class="flex flex-wrap items-center justify-center h-full text-gray-800 g-6">
                        <div class="mb-12 md:w-8/12 lg:w-6/12 md:mb-0">
                            <img src="https://mdbcdn.b-cdn.net/img/Photos/new-templates/bootstrap-login-form/draw2.svg"
                                class="w-full" alt="Phone image" />
                        </div>
                        <div class="md:w-8/12 lg:w-5/12 lg:ml-20">
                            <div v-if="_error">
                                <p class="p-3 mb-5 text-sm text-red-200 bg-red-500">
                                    {{ _error }}
                                </p>
                            </div>
                            <form @submit.prevent="onSubmit">
                                <!-- Email input -->
                                <div class="mb-6">
                                    <input type="text"
                                        class="block w-full px-4 py-2 m-0 text-xl font-normal text-gray-700 transition ease-in-out bg-white border border-gray-300 border-solid rounded form-control bg-clip-padding focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
                                        placeholder="Email address" v-model="form.email" />
                                </div>

                                <!-- Password input -->
                                <div class="mb-6">
                                    <input type="password"
                                        class="block w-full px-4 py-2 m-0 text-xl font-normal text-gray-700 transition ease-in-out bg-white border border-gray-300 border-solid rounded form-control bg-clip-padding focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
                                        placeholder="Password" v-model="form.password" />
                                </div>

                                <!-- Submit button -->
                                <button type="submit"
                                    class="inline-block w-full py-3 text-sm font-medium leading-snug text-white uppercase transition duration-150 ease-in-out bg-blue-600 rounded shadow-md px-7 hover:bg-blue-700 hover:shadow-lg focus:bg-blue-700 focus:shadow-lg focus:outline-none focus:ring-0 active:bg-blue-800 active:shadow-lg"
                                    data-mdb-ripple="true" data-mdb-ripple-color="light">
                                    <span v-if="isLoading">Loading...</span>
                                    <span v-else>Sign in</span>
                                </button>
                            </form>
                        </div>
                    </div>
                </div>
            </section>
        </div>
    </div>
</template>

<script setup>
import { useAuth } from "~~/composables/states"

const url = "https://reqres.in/api/login"

const isLoading = ref(false)
const _error = ref(null)

const form = reactive({
    email: 'eve.holt@reqres.in',
    password: 'cityslicka'
})

async function onSubmit() {
    if (isLoading.value) return

    isLoading.value = true
    const { data, error } = await useFetch(url, {
        method: 'post',
        body: form
    })
    isLoading.value = false
    if (error.value) {
        _error.value = error.value.data.error
        return
    }

    const auth = useAuth()
    auth.value.isAuthenticated = true
    navigateTo('/')
}
</script>