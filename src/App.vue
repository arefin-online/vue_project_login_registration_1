<script setup>
import { ref } from 'vue'

const year = (new Date()).getFullYear()
const validUsername = "arefin"
const validPassword = "1234"

const uname = ref("")
const upass = ref("")

const pageTitle = "CodeWithArefin"
const imageURL = "https://images.unsplash.com/photo-1470252649378-9c29740c9fa8?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1740&q=80"

const titleUsername = "Username"
const titlePassword = "Password"
const titleRetypePassword = "Retype Password"
const placeholderTextUsername = "Username"
const placeholderTextPassword = "********"
const placeholderTextRetypePassword = "********"
const loginTitle = "Login"
const registerTitle = "Register"
const loginButton = "Sign In"
const registerButton = "Register"
const copyrightText = `\u00A9 ${year} ${pageTitle}. All rights reserved.`

const loginDisplay = ref("show")
const registerDisplay = ref("hide")

const successShow = ref("")
const err_username = ref("display:none")
const err_password = ref("display:none")
const err_username_message = ref("")
const err_password_message = ref("")

function showLogin() {
    loginDisplay.value = "show"
    registerDisplay.value = "hide"
}

function showRegister() {
    loginDisplay.value = "hide"
    registerDisplay.value = "show"
}

function hideAll() {
    loginDisplay.value = "hide"
    registerDisplay.value = "hide"
    successShow.value = "You have logged in successfully!"
}

function matchUsername() {

    if(uname.value === "") {
        err_username.value="display:block"
        err_username_message.value = "Please choose a username"
    } else if(uname.value !== validUsername) {
        err_username.value="display:block"
        err_username_message.value = "Username is invalid"
    }

    if(upass.value === "") {
        err_password.value="display:block"
        err_password_message.value = "Please choose a password"
    } else if(upass.value !== validPassword) {
        err_password.value="display:block"
        err_password_message.value = "Password is invalid"
    }

    if(uname.value === validUsername && upass.value === validPassword) {
        hideAll();
    } else if(uname.value === validUsername) {
        err_username.value="display:none"
    } else if(upass.value === validPassword) {
        err_password.value="display:none"
    }
}


</script>

<template>
    <section class="flex h-screen w-full">
        <div class="w-1/2" style="background-repeat: no-repeat; background-size: cover;" :style="[{backgroundImage: 'url('+imageURL+')'}]">
            <h1 class="mb-5 text-2xl mt-10 ml-10 text-white">{{ pageTitle }}</h1>
        </div>
        <div class="w-1/2 flex flex-col justify-center items-center bg-gray-200">

            <div class="mb-5 text-xl text-green-700">{{ successShow }}</div>

            <h2 class="mb-5 text-xl" :class="'login_'+loginDisplay">{{ loginTitle }}</h2>
            <div class="w-full max-w-xs" :class="'login_'+loginDisplay">
                <form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
                    <div class="mb-4">
                        <label class="block text-gray-700 text-sm font-bold mb-2" for="username">
                            {{ titleUsername }}
                        </label>
                        <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="username" type="text" :placeholder="placeholderTextUsername" v-model="uname">
                        <p class="text-red-500 text-xs italic" :style="err_username">{{ err_username_message }}</p>
                    </div>
                    <div class="mb-6">
                        <label class="block text-gray-700 text-sm font-bold mb-2" for="password">
                            {{ titlePassword }}
                        </label>
                        <input class="shadow appearance-none border  rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline" id="password" type="password" :placeholder="placeholderTextPassword" v-model="upass">
                        <p class="text-red-500 text-xs italic" :style="err_password">{{ err_password_message }}</p>
                    </div>
                    <div class="flex items-center justify-between">
                        <button @click="matchUsername()" class="bg-orange-600 hover:bg-orange-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" type="button">
                            {{ loginButton }}
                        </button>
                        <a @click="showRegister()" class="inline-block align-baseline font-bold text-sm text-orange-600 hover:text-orange-800" href="#">
                            Or {{ registerButton }}
                        </a>
                    </div>
                </form>
            </div>




            <h2 class="mb-5 text-xl" :class="'register_'+registerDisplay">{{ registerTitle }}</h2>
            <div class="w-full max-w-xs" :class="'register_'+registerDisplay">
                <form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
                    <div class="mb-4">
                        <label class="block text-gray-700 text-sm font-bold mb-2" for="username">
                            {{ titleUsername }}
                        </label>
                        <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="username" type="text" :placeholder="placeholderTextUsername">
                    </div>
                    <div class="mb-4">
                        <label class="block text-gray-700 text-sm font-bold mb-2" for="password">
                            {{ titlePassword }}
                        </label>
                        <input class="shadow appearance-none border  rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline" id="password" type="password" :placeholder="placeholderTextPassword">

                    </div>
                    <div class="mb-6">
                        <label class="block text-gray-700 text-sm font-bold mb-2" for="retype password">
                            {{ titleRetypePassword }}
                        </label>
                        <input class="shadow appearance-none border  rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline" id="retypePassword" type="password" :placeholder="placeholderTextRetypePassword">
                        <!-- <p class="text-red-500 text-xs italic">Please choose a password.</p> -->
                    </div>
                    <div class="flex items-center justify-between">
                        <button class="bg-orange-600 hover:bg-orange-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" type="button">
                            {{ registerButton }}
                        </button>
                        <a @click="showLogin()" class="inline-block align-baseline font-bold text-sm text-orange-600 hover:text-orange-800" href="#">
                            Or {{ loginButton }}
                        </a>
                    </div>
                </form>
            </div>






            <div class="w-full max-w-xs">
                <p class="text-center text-gray-500 text-xs">
                    {{ copyrightText }}
                </p>
            </div>

        </div>
    </section>
</template>

<style scoped>
.login_show {display: block;}
.login_hide {display: none;}
.register_show {display: block;}
.register_hide {display: none;}

</style>