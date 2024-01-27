<template>
  <div class="checkbox-list">
    <my-checkbox :checkboxes="checkboxItem">
      <p>«Я принимаю <a>лицензионное
          соглашение</a>».</p>
    </my-checkbox>
    <my-checkbox @checkbox-changed="renderlist" :checkboxes="checkboxList" />
    <h3 class="checkbox-list__title">Список активных чекбоксов:</h3>
    <ul class="checkbox-list__list">
      <li class="checkbox-list__item" v-for="selectedItemId in checkboxNewList" :key="selectedItemId">
        {{ getItemById(selectedItemId) }}
      </li>
    </ul>
  </div>
</template>

<script>
import MyCheckbox from "@/components/UI/MyCheckbox.vue";

export default {
  components: { MyCheckbox },
  props: {
    checkboxList: {
      type: Array,
    },
    checkboxItem: {
      type: Array,
    }
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
  box-sizing: border-box;
}

.checkbox-list__title {
  margin-bottom: 10px;
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

.checkbox-list__list {
  list-style: none;
  margin: 0;
  display: flex;
  gap: 10px;
}

.checkbox-list__item {

  color: #fff;
}
</style>
