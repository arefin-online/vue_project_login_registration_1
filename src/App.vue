<script setup>
import { ref } from 'vue'

const year = (new Date()).getFullYear()

const validUsername = ref("admin")
const validPassword = ref("1234")

const uName = ref("")
const uPass = ref("")
const uNameR = ref("")
const uPassR = ref("")
const uRPassR = ref("")

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
const logout_status = ref("display:none")

const successShowR = ref("")
const err_username_r = ref("display:none")
const err_password_r = ref("display:none")
const err_re_password_r = ref("display:none")
const err_username_message_r = ref("")
const err_password_message_r = ref("")
const err_re_password_message_r = ref("")
const back_status_r = ref("display:none")

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
    logout_status.value = "display:block"
}
function hideAllR() {
    loginDisplay.value = "hide"
    registerDisplay.value = "hide"
    successShowR.value = "Thank you for registering"
    back_status_r.value = "display:block"
}
function logout() {
    loginDisplay.value = "show"
    registerDisplay.value = "hide"
    successShow.value = ""
    logout_status.value = "display:none"
}
function backR() {
    loginDisplay.value = "show"
    registerDisplay.value = "hide"
    successShowR.value = ""
    back_status_r.value = "display:none"
}


function matchData() {

    if(uName.value === "") {
        err_username.value="display:block"
        err_username_message.value = "Please choose a username"
    } else if(uName.value !== validUsername.value) {
        err_username.value="display:block"
        err_username_message.value = "Username is invalid"
    }

    if(uPass.value === "") {
        err_password.value="display:block"
        err_password_message.value = "Please choose a password"
    } else if(uPass.value !== validPassword.value) {
        err_password.value="display:block"
        err_password_message.value = "Password is invalid"
    }

    if(uName.value === validUsername.value && uPass.value === validPassword.value) {
        hideAll();
    } else if(uName.value === validUsername.value) {
        err_username.value="display:none"
    } else if(uPass.value === validPassword.value) {
        err_password.value="display:none"
    }
}


function matchDataR() {

    if(uNameR.value !== "" && uPassR.value !== "" && uRPassR.value !== "") {
        hideAllR();
        // Reset the username and passwords
        validUsername.value = uNameR.value
        validPassword.value = uPassR.value
        uName.value = validUsername.value
        uPass.value = validPassword.value
    }

    if(uNameR.value === "") {
        err_username_r.value="display:block"
        err_username_message_r.value = "Please choose a username"
    }

    if(uPassR.value === "") {
        err_password_r.value="display:block"
        err_password_message_r.value = "Please choose a password"
    }

    if(uRPassR.value === "") {
        err_re_password_r.value="display:block"
        err_re_password_message_r.value = "Please choose a password"
    }
}

</script>

<template>
    <section class="flex h-screen w-full">

        <div class="w-1/2" style="background-repeat: no-repeat; background-size: cover;" :style="[{backgroundImage: 'url('+imageURL+')'}]">
            <h1 class="mb-5 text-2xl mt-10 ml-10 text-white">{{ pageTitle }}</h1>
        </div>

        <div class="w-1/2 flex flex-col justify-center items-center bg-gray-200">

            <!-- Success Message -->
            <div class="mb-5 text-xl text-green-700">{{ successShow }}</div>
            <div class="mb-5 cursor-pointer bg-orange-600 hover:bg-orange-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" :style="logout_status" @click="logout()">Logout</div>


            <!-- Success Message -->
            <div class="mb-5 text-xl text-green-700">{{ successShowR }}</div>
            <div class="mb-5 cursor-pointer bg-orange-600 hover:bg-orange-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" :style="back_status_r" @click="backR()">Back</div>


            <!-- Login Form -->
            <h2 class="mb-5 text-xl" :class="'login_'+loginDisplay">{{ loginTitle }}</h2>
            <div class="w-full max-w-xs" :class="'login_'+loginDisplay">
                <form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
                    <div class="mb-4">
                        <label class="block text-gray-700 text-sm font-bold mb-2" for="username">
                            {{ titleUsername }}
                        </label>
                        <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="usernameLogin" type="text" :placeholder="placeholderTextUsername" v-model="uName">
                        <p class="text-red-500 text-xs italic" :style="err_username">{{ err_username_message }}</p>
                    </div>
                    <div class="mb-6">
                        <label class="block text-gray-700 text-sm font-bold mb-2" for="password">
                            {{ titlePassword }}
                        </label>
                        <input class="shadow appearance-none border  rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline" id="passwordLogin" type="password" :placeholder="placeholderTextPassword" v-model="uPass">
                        <p class="text-red-500 text-xs italic" :style="err_password">{{ err_password_message }}</p>
                    </div>
                    <div class="flex items-center justify-between">
                        <button @click="matchData()" class="bg-orange-600 hover:bg-orange-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" type="button">
                            {{ loginButton }}
                        </button>
                        <a @click="showRegister()" class="inline-block align-baseline font-bold text-sm text-orange-600 hover:text-orange-800" href="javascript:void;">
                            Or {{ registerButton }}
                        </a>
                    </div>
                </form>
            </div>



            <!-- Registration Form -->
            <h2 class="mb-5 text-xl" :class="'register_'+registerDisplay">{{ registerTitle }}</h2>
            <div class="w-full max-w-xs" :class="'register_'+registerDisplay">
                <form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
                    <div class="mb-4">
                        <label class="block text-gray-700 text-sm font-bold mb-2" for="username for register">
                            {{ titleUsername }}
                        </label>
                        <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="usernameRegister" type="text" :placeholder="placeholderTextUsername" v-model="uNameR">
                        <p class="text-red-500 text-xs italic" :style="err_username_r">{{ err_username_message_r }}</p>
                    </div>
                    <div class="mb-4">
                        <label class="block text-gray-700 text-sm font-bold mb-2" for="password for register">
                            {{ titlePassword }}
                        </label>
                        <input class="shadow appearance-none border  rounded w-full py-2 px-3 text-gray-700  leading-tight focus:outline-none focus:shadow-outline" id="passwordRegister" type="password" :placeholder="placeholderTextPassword" v-model="uPassR">
                        <p class="text-red-500 text-xs italic" :style="err_password_r">{{ err_password_message_r }}</p>
                    </div>
                    <div class="mb-6">
                        <label class="block text-gray-700 text-sm font-bold mb-2" for="retype password for register">
                            {{ titleRetypePassword }}
                        </label>
                        <input class="shadow appearance-none border  rounded w-full py-2 px-3 text-gray-700  leading-tight focus:outline-none focus:shadow-outline" id="retypePasswordRegister" type="password" :placeholder="placeholderTextRetypePassword" v-model="uRPassR">
                        <p class="text-red-500 text-xs italic" :style="err_re_password_r">{{ err_re_password_message_r }}</p>
                    </div>
                    <div class="flex items-center justify-between">
                        <button @click="matchDataR()" class="bg-orange-600 hover:bg-orange-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" type="button">
                            {{ registerButton }}
                        </button>
                        <a @click="showLogin()" class="inline-block align-baseline font-bold text-sm text-orange-600 hover:text-orange-800" href="javascript:void;">
                            Or {{ loginButton }}
                        </a>
                    </div>
                </form>
            </div>



            <!-- Default Username and Password -->
            <div class="default-value text-sm mb-4">
                Default Username: {{ validUsername }}<br>
                Default Password: {{ validPassword }}
            </div>


            <!-- Copyright Text -->
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