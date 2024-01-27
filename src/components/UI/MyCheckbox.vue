<template>
  <template v-for="checkbox in checkboxes" :key="checkbox.id">
    <div v-if="checkbox.visible" class="checkbox-wrapper">
      <input v-model="selectedCheckboxes" :disabled="checkbox.disabled" :value="checkbox.id" class="my-checkbox"
        type="checkbox" @change="updateInput()" :id="checkbox.id">
      <label class="checkbox-label" v-bind:for="checkbox.id">
        {{ checkbox.title }} <slot></slot>
      </label>
    </div>
  </template>
</template>
<script>
export default {
  name: 'MyCheckbox',
  props: {
    checkboxes: {
      type: Array,
      required: true,
    },
  },
  emits: ['checkbox-changed'],
  data() {
    return {
      selectedCheckboxes: []
    }
  },
  methods: {
    updateInput() {
      this.$emit('checkbox-changed', this.selectedCheckboxes)
      console.log(this.selectedCheckboxes)
    },
  }
}
</script>

<style scoped>
.checkbox-wrapper {
  margin-top: 20px;
  display: flex;
}

.my-checkbox {
  display: none;
}

.checkbox-label {
  display: inline-block;
  cursor: pointer;
  position: relative;
  padding-left: 30px;
  margin-right: 0;
  user-select: none;

  font-family: "Gotham Pro";
  font-size: 12px;
  font-style: normal;
  font-weight: 400;
  line-height: 16px;
  letter-spacing: 0.396px;
  color: white;

}

.checkbox-label::before {
  content: "";
  display: inline-block;
  width: 23px;
  height: 23px;
  position: absolute;
  left: 0;
  bottom: 0;
  background: url('../../images/checkbox.svg') 0 0 no-repeat;
}

input[type=checkbox]:disabled:checked+.checkbox-label::before {
  background: url('../../images/checkbox-disabled-on.svg') 0 0 no-repeat;
}

input[type=checkbox]:disabled+.checkbox-label::before {
  background: url('../../images/checkbox-disabled-off.svg') 0 0 no-repeat;
}

.checkbox-label:target::before {
  background: url('../../images/checkbox-active-off.svg') 0 0 no-repeat;
}

input[type=checkbox]:not(:disabled):checked:active+.checkbox-label::before {
  background: url('../../images/checkbox-active-on.svg') 0 0 no-repeat;
}

input[type=checkbox]:not(:disabled):active+.checkbox-label::before {
  background: url('../../images/checkbox-active-off.svg') 0 0 no-repeat;
}

input[type=checkbox]:checked+.checkbox-label::before {
  background: url('../../images/checkbox-off.svg') 0 0 no-repeat;
}


.checkbox-label:hover::before {
  background: url('../../images/checkbox-off-hover.svg') 0 0 no-repeat;
}


input[type=checkbox]:checked+.checkbox-label:hover::before {
  background: url('../../images/checkbox-on-hover.svg') 0 0 no-repeat;
}
</style>
