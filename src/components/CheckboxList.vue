<template>
    <div class="checkbox-list">
        <h3>Список чекбоксов</h3>
        <MyCheckbox :checkbox="{ id: '01', visible: true }">
            <p>Я принимаю <a>лицензионное соглашение</a></p>
        </MyCheckbox>
        <MyCheckbox v-for="checkbox in checkboxList" :checkbox="checkbox" :key="checkbox.id" v-model="checkboxNewList"
            @renderlist="renderlist"></MyCheckbox>
        <ul>
            <li v-for="selectedItemId in checkboxNewList" :key="selectedItemId">
                {{ getItemById(selectedItemId) }}
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    props: {
        checkboxList: {
            type: Array,
            required: true,
        },
    },
    data() {

        return {

            checkboxNewList: []
        }
    },
    methods: {
        renderlist(checkboxList) {
            this.checkboxNewList = this.checkboxList
        },

        getItemById(id) {
            const selectedItem = this.checkboxNewList.find(item => item.id === id);
            return selectedItem ? selectedItem.title : ''
        }


    }
}


</script>

<style scoped>
.checkbox-list {
    padding: 20px;
    background-color: black;
}
</style>