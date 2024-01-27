<template>
  <div class="checkbox-list">
    <my-checkbox @checkbox-changed="renderlist" :checkboxes="checkboxList" />
    <h3 class="checkbox__title">Список активных чекбоксов:</h3>
    <ul>
      <li class="checkbox__item" v-for="selectedItemId in checkboxNewList" :key="selectedItemId">
        {{ getItemById(selectedItemId) }}
      </li>
    </ul>
  </div>
</template>

<script>
import MyCheckbox from "@/components/UI/MyCheckbox.vue";

export default {
  components: {MyCheckbox},
  props: {
    checkboxList: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      checkboxNewList: [],
    }
  },
  methods: {
    renderlist(checkboxList) {
      this.checkboxNewList = checkboxList
      console.log(this.checkboxNewList)
    },

    getItemById(id) {
      const selectedItem = this.checkboxList.find(item => item.id === id);
      return selectedItem ? selectedItem.title : ''
    }


  }
}

</script>

<style scoped>
.checkbox-list {
  padding: 20px;
  background-color: black;
  color: #fff;
}

.checkbox__title {
  margin-bottom: 10px;
}

.checkbox__item {
  color: #fff;
}
</style>
