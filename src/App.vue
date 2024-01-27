<template>
    <div class="app">
        <h1 class="title">Тестовое задание</h1>

        <section class="section">
            <h2 class="section__title">Задание №1</h2>
            <CheckboxList v-model:checkboxList="checkboxList" v-model:checkboxItem="checkboxItem"></CheckboxList>
        </section>

        <section class="section">
            <h2 class="section__title">Задание №2</h2>
            <MySelectVue :options="options" v-model="parrentSelectedOption"></MySelectVue>
            <p class="dropdown__caption">Выбрана опция: {{ this.parrentSelectedOption.name }}</p>
        </section>

    </div>
</template>

<script>
import CheckboxList from '@/components/CheckboxList'
import MySelectVue from '@/components/UI/MySelect'
import axios from 'axios'

import { ref } from 'vue';




export default {
    components: {
        CheckboxList, MySelectVue
    },
    data() {
        return {
            checkboxItem: [{
                "id": 10,
                "visible": true,
            }],
            checkboxList: [
                {
                    "id": 1,
                    "title": "apple",
                    "visible": true,
                    "disabled": true,

                },
                {
                    "id": 2,
                    "title": "melon",
                    "visible": false,

                },
                {
                    "id": 3,
                    "title": "pineapple",
                    "visible": true,

                },
                {
                    "id": 4,
                    "title": "banana",
                    "visible": true,

                },
                {
                    "id": 5,
                    "title": "watermelon",
                    "visible": true,

                }
            ],
            options: ref([
                {
                    name: 'Первый',
                    value: 1,
                    pressed: false,
                    state: 'Normal',
                    icon: false
                },
                {
                    name: 'Второй',
                    value: 2,
                    pressed: false,
                    state: 'Normal',
                    icon: false
                }, {
                    name: 'Третий',
                    value: 3,
                    pressed: false,
                    state: 'Normal',
                    icon: false
                }, {
                    name: 'Четвертый',
                    value: 4,
                    pressed: false,
                    state: 'Disabled',
                    icon: false
                }, {
                    name: 'Пятый',
                    value: 5,
                    pressed: false,
                    state: 'Disabled',
                    icon: true
                },
                {
                    name: 'Шестой',
                    value: 6,
                    pressed: false,
                    state: 'Normal',
                    icon: true
                }]),
            parrentSelectedOption: ref({})

        }
    },

}
</script>

<style>
@import url(./variabels/variables.css);

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.app {
    padding: 20px;
    background-color: black;
    height: 100%;
    box-sizing: border-box;
}

.title {
    display: block;
    font-size: 36px;
    font-family: "Gotham Pro";
    font-style: normal;
    font-weight: 500;
    letter-spacing: 0.252px;
    text-align: center;
    color: var(--gradients-white);
}

.section {
    width: 90%;
    display: flex;
    flex-direction: column;
    margin: 20px auto;
    border: 2px var(--secondary-secondary500) dashed;
    border-radius: 10px;
    overflow: hidden;
}

.section__title {
    display: block;
    font-size: 24px;
    font-family: "Gotham Pro";
    font-style: normal;
    font-weight: 500;
    letter-spacing: 0.252px;
    text-align: center;
    color: var(--gradients-white);
    margin: 20px 0;
}

.dropdown__caption {
    font-size: 16px;
    font-family: "Gotham Pro";
    font-style: normal;
    font-weight: 400;
    letter-spacing: 0.252px;
    text-align: center;
    color: var(--gradients-white);
    margin: 20px 0;
}
</style>