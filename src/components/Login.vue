<template>
    <div :class="{ 'hidden': hiddenStore.login }"
        class=" overflow-y-auto overflow-x-hidden fixed top-0 right-0 sm:left-40 z-50 justify-center items-center w-full inset-0 h-[calc(100%-1rem)] max-h-[450px] max-w-2xl mx-auto">
        <div class="relative p-4 w-full max-w-2xl max-h-full">
            <div class="relative bg-white rounded-lg shadow">
                <div class="flex items-center justify-between p-4 p-5 border-b rounded-t">
                    <h3 class="text-xl font-semibold text-gray-900">
                        Авторизация
                    </h3>
                    <button @click="hiddenStore.showLogin()"
                        class="end-2.5 text-gray-400 bg-transparent hover:bg-gray-200 hover:text-gray-900 rounded-lg text-sm w-8 h-8 ms-auto inline-flex justify-center items-center">
                        <svg class="w-3 h-3" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 14 14">
                            <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                d="m1 1 6 6m0 0 6 6M7 7l6-6M7 7l-6 6" />
                        </svg>
                    </button>
                </div>

                <!-- Login -->
                <div class="p-4 p-5" v-if="showing == 'log' && userStore.userID == 1">
                    <a class="space-y-4">
                        <label class="block mb-2 text-sm font-medium text-gray-900">Вход</label>
                        <div>
                            <input type="email" v-model="enterData[0]"
                                class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
                                placeholder="Логин">
                        </div>

                        <div>
                            <input :type="inputType" placeholder="Пароль" v-model="enterData[1]"
                                class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5">
                        </div>

                        <div class="flex items-start mb-5">
                            <div class="flex items-center h-5">
                                <input type="checkbox" v-model="checkbox"
                                    class="w-4 h-4 border border-gray-300 rounded bg-gray-50 focus:ring-3 focus:ring-blue-300 dark:bg-gray-700 dark:border-gray-600 dark:focus:ring-blue-600 dark:ring-offset-gray-800 dark:focus:ring-offset-gray-800">
                            </div>
                            <label class="ms-2 text-sm font-medium text-gray-900 dark:text-gray-300">Показать
                                пароль</label>
                        </div>

                        <button @click="enter(enterData)"
                            class="w-full text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center">Войти</button>
                        <div class="text-sm font-medium text-gray-500">
                            Не зарегистрированы? <button @click="showing = 'reg'"
                                class="text-blue-700 hover:underline">Создать аккаунт</button>
                        </div>
                    </a>
                </div>
                <!-- -->

                <!-- Registration -->
                <div class="p-4 p-5" v-if="showing == 'reg' && userStore.userID == 1">
                    <a class="space-y-4">
                        <label class="block mb-2 text-sm font-medium text-gray-900">Регистрация</label>
                        <div>
                            <input type="email" v-model="regData[0]"
                                class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
                                placeholder="Логин">
                        </div>

                        <div>
                            <input :type="inputType" placeholder="Пароль" v-model="regData[1]"
                                class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5">
                        </div>


                        <div class="flex items-start mb-5">
                            <div class="flex items-center h-5">
                                <input type="checkbox" v-model="checkbox"
                                    class="w-4 h-4 border border-gray-300 rounded bg-gray-50 focus:ring-3 focus:ring-blue-300 dark:bg-gray-700 dark:border-gray-600 dark:focus:ring-blue-600 dark:ring-offset-gray-800 dark:focus:ring-offset-gray-800">
                            </div>
                            <label class="ms-2 text-sm font-medium text-gray-900 dark:text-gray-300">Показать
                                пароль</label>
                        </div>


                        <button type="submit" @click="registration(regData)"
                            class="w-full text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center">Создать
                            аккаунт</button>
                        <div class="text-sm font-medium text-gray-500">
                            Уже есть аккаунт? <button @click="showing = 'log'" class="text-blue-700 hover:underline">
                                Войти</button>
                        </div>
                    </a>
                </div>

                <!-- Account -->
                <div class="flex flex-col items-center pb-10 pt-10" v-if="userStore.userID > 1 && showing != 'edit'">
                    <img class="w-24 h-24 mb-3 rounded-full shadow-lg" src="../assets/avatar.png" />
                    <h5 class="mb-1 text-xl font-medium text-gray-900">{{ userStore.userLogin }}</h5>
                    <span class="text-sm text-gray-500">ID: {{ userStore.userID }}</span>
                    <div class="flex mt-6">
                        <button @click="exit()"
                            class="inline-flex items-center px-4 py-2 text-sm font-medium text-center text-white bg-blue-700 rounded-lg hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300">
                            Выйти
                        </button>
                        <button @click="showing = 'edit'"
                            class="py-2 px-4 ms-2 text-sm font-medium text-gray-900 focus:outline-none bg-white rounded-lg border border-gray-200 hover:bg-gray-100 hover:text-blue-700 focus:ring-4 focus:ring-gray-100">
                            Сменить пароль
                        </button>
                    </div>

                    <button @click="deleteAccount()"
                        class="py-2 px-14 mt-2 text-sm font-medium focus:outline-none bg-red-50 rounded-lg border border-red-500 text-red-700 hover:bg-red-150 hover:text-red-900 focus:ring-4 focus:ring-gray-100">
                        Удалить аккаунт
                    </button>
                </div>

                <!-- editPassword -->
                <div class="p-4 p-5" v-if="showing == 'edit' && userStore.userID > 1">
                    <a class="space-y-4">
                        <label class="block mb-2 text-sm font-medium text-gray-900">Смена пароля</label>
                        <div>
                            <input :type="inputType" placeholder="Новый пароль" v-model="editPassData[0]"
                                class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5">
                        </div>

                        <div>
                            <input :type="inputType" placeholder="Повторите пароль" v-model="editPassData[1]"
                                class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5">
                        </div>

                        <div class="flex items-start mb-5">
                            <div class="flex items-center h-5">
                                <input type="checkbox" v-model="checkbox"
                                    class="w-4 h-4 border border-gray-300 rounded bg-gray-50 focus:ring-3 focus:ring-blue-300 dark:bg-gray-700 dark:border-gray-600 dark:focus:ring-blue-600 dark:ring-offset-gray-800 dark:focus:ring-offset-gray-800">
                            </div>
                            <label class="ms-2 text-sm font-medium text-gray-900 dark:text-gray-300">Показать
                                пароль</label>
                        </div>

                        <button @click="editPassword(editPassData)"
                            class="w-full text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center">Сменить
                            пароль</button>





                        <div class="text-sm font-medium text-gray-500">
                            <button @click="showing = 'reg'" class="text-blue-700 hover:underline">
                                Назад</button>
                        </div>

                    </a>
                </div>

            </div>
        </div>
    </div>
</template>


<script setup>
import { ref, watch } from 'vue'
import { useComponents } from '../../store/ComponentsHidden';
import { useUser } from '../../store/User';
import axios from 'axios';
defineProps({
    msg: String,
})
const hiddenStore = useComponents();
const userStore = useUser();
const showing = ref('reg')

const regData = ref([])
const enterData = ref([])
const editPassData = ref([])


const checkbox = ref(false)
const inputType = ref("password")


watch(checkbox, () => {
    if (checkbox.value === true) {
        inputType.value = "text"
    }
    if (checkbox.value === false) {
        inputType.value = "password"
    }
})



function registration(value) {
    axios.get(`https://dexone.ru/backend_fuelly/users`).then((res) => {
        let lastId = Number(res.data[res.data.length - 1].id) //последний зарегистрированный id

        let logins = [] //массив логинов
        for (let i = 0; i < res.data.length; i++) {
            logins.push(res.data[i].login)
        }

        if (logins.includes(value[0]) == false) { //если логин не найден в бд допускается регистрация
            axios.post(`https://dexone.ru/backend_fuelly/users`, { id: lastId + 1, login: value[0], password: value[1] }) //создание пользователя
            axios.post(`https://dexone.ru/backend_fuelly/data`, { id: lastId + 1, car: "Unnamed Car", cost: "50", maslo: "0", svechi: "0", masloAKPP: "0", toplFilter: "0", tormozn: "0", info: [] }) //создание data
            userStore.userID = lastId + 1 //задает id нового пользователя в сторе
            userStore.userLogin = value[0] //задается login пользователя в сторе
            setTimeout(() => {
                userStore.updateInfo()
            }, 1000);
        }
        else {
            alert("Такой пользователь существует")
        }
    })

}

function enter(value) {
    axios.get(`https://dexone.ru/backend_fuelly/users`).then((res) => {
        let logins = []
        let passwords = []
        for (let i = 0; i < res.data.length; i++) {
            logins.push(res.data[i].login) //массив логинов в дб
            passwords.push(res.data[i].password) //массив паролей в дб
        }
        let search = logins.indexOf(value[0]); //возврат индекса введенного логина в базе данных или -1 если нет
        if (search > 0 && res.data[search].password == value[1]) { //если найден логин и пароль по этому индексу равен введенному value то
            userStore.userID = res.data[search].id //задается id пользователя в сторе
            userStore.userLogin = res.data[search].login //задается login пользователя в сторе
            userStore.updateInfo()
        }
        else {
            alert("Неверный логин или пароль")
        }
    })
}

function exit() {
    userStore.userID = 1 //задается id пользователя в сторе
    userStore.userLogin = "guest" //задается login пользователя в сторе
    userStore.updateInfo()
}

function deleteAccount() {
    axios.delete(`https://dexone.ru/backend_fuelly/users/${userStore.userID}`) //удаление user
    axios.delete(`https://dexone.ru/backend_fuelly/data/${userStore.userID}`) //удаление data
    userStore.userID = 1 //задается id пользователя в сторе
    userStore.userLogin = "guest" //задается login пользователя в сторе
    userStore.updateInfo()
}

function editPassword(value) {
    if (value[0] == value[1]) { //если пароль и повтор пароля совпадают
        axios.patch(`https://dexone.ru/backend_fuelly/users/${userStore.userID}`, { password: value[0] }) //изменение пароля
        value[0] = ""
        value[1] = ""
        alert("Пароль изменен")
    }
    else {
        alert("Пароли не совпадают")
    }
}
</script>