<template>
    <div class="app">
        <h1>Страница с постами</h1>
        <MyButton @click="showDialog">Создать пост</MyButton>
        <MyDialog v-model:show="dialogVisible">
            <PostForm @create="createPost"></PostForm>
        </MyDialog>

        <PostList :posts="posts" @remove="removePosts"></PostList>
    </div>

    <CheckboxList v-model:checkboxList="checkboxList"></CheckboxList>
    <MySelectVue :options="options" v-model="parrentSelectedOption"></MySelectVue>
    <h1>Выбрана опция: {{ this.parrentSelectedOption.name }}</h1>
</template>

<script>
import PostForm from '@/components/PostForm'
import PostList from '@/components/PostList'
import CheckboxList from '@/components/CheckboxList'
import MySelectVue from '@/components/UI/MySelect'
import axios from 'axios'

import { ref } from 'vue';




export default {
    components: {
        PostForm, PostList, CheckboxList, MySelectVue
    },
    data() {
        return {
            posts: [],
            dialogVisible: false,
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
                    value: 1
                },
                {
                    name: 'Второй',
                    value: 2
                }, {
                    name: 'Третий',
                    value: 3
                }, {
                    name: 'Четвертый',
                    value: 4
                }, {
                    name: 'Пятый',
                    value: 5
                },
                {
                    name: 'Шестой',
                    value: 6
                }]),
                parrentSelectedOption: ref({})

        }
    },
    methods: {

        createPost(post) {
            this.posts.push(post);
            this.dialogVisible = false;
        },
        removePosts(post) {
            this.posts = this.posts.filter(p => p.id !== post.id)
        },
        showDialog() {
            this.dialogVisible = true;
        },
        async fetchPosts() {
            try {
                const res = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10');
                console.log(res)
                this.posts = res.data;
            } catch (error) {
                alert(error)
            }

        },

    },
    mounted() {
        this.fetchPosts();
    }
}
</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.app {
    padding: 20px;
}
</style>