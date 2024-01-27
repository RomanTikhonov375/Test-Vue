<template>
    <div class="dropdown" ref="dropDown">
        <div class="dropdown__button" @click="isDropDownVisible = !isDropDownVisible" ref="dropdownButton">
        </div>
        <Transition name="slide-fade">
            <div :class="`dropdown__options-wrapper ${calcButtonPlace}`" v-if="isDropDownVisible">
                <div class="dropdown__option"
                    v-bind:class="[{ 'dropdown__option-pressed': option.pressed }, option.state === 'Disabled' ? 'dropdown__option-disabled' : '']"
                    v-for="(option, index) in props.options" :key="index" @click="toggleOptionSelect(option)">
                    <div class="dropdown__option-icon" v-if="option.icon"></div>
                    <p class="dropdown__option-text">{{ option.name || option }}</p>
                </div>
            </div>
        </Transition>


    </div>
</template>

<script setup>
import { computed, defineProps, ref, defineEmits, onMounted, onBeforeUnmount } from 'vue';

const props = defineProps({
    options: {
        type: Array,
        reqired: true,
    },
    modelValue: {
        default: null
    }
})

const selecredOption = ref(null)
const dropDown = ref(null)
const dropdownButton = ref(null)
const emit = defineEmits(['update:modelValue'])


const toggleOptionSelect = (option) => {
    if (option.state === 'Normal') {
        clearPressedOptions();
        selecredOption.value = option
        emit('update:modelValue', option)
        option.pressed = true;
    }

}

const clearPressedOptions = () => {
    props.options.forEach(option => {
        option.pressed = false
    });
}

const mappedSelectedOption = computed(() => {
    return (selecredOption.value?.name || selecredOption.value) || 'Выберите опцию'
})

const isDropDownVisible = ref(false)

const onCloseDropDown = (element) => {
    if (!dropDown.value.contains(element.target)) {
        isDropDownVisible.value = false
       
    }
}

const calcButtonPlace = computed(() => {
    const coordinatesButton = dropdownButton.value.getBoundingClientRect() 
      const windowWidth = window.innerWidth;
      const windowHeight = window.innerHeight;
      const {x, y} = coordinatesButton;
      console.log(x, y, windowWidth, windowHeight)
      console.log(windowHeight / 2 > y)

      if (windowWidth / 2 > x) {
        if (windowHeight / 2 > y) { 
          return 'bottomRight'
        } else { 
          return 'topRight'
        }
      } else {
        if (windowHeight / 2 > y) { 
          return 'bottomLeft'
        } else { // 
          return 'topLeft'
        }
      }
  })

onMounted(() => {
    window.addEventListener('click', onCloseDropDown)
})

onBeforeUnmount(() => {
    window.removeEventListener('click', onCloseDropDown)
})


</script>

<style scoped>
.dropdown {
    width: 24px;
    margin-left: 20px;
    position: relative;
}

.dropdown__button {
    cursor: pointer;
    width: 24px;
    height: 24px;
    background: url('../../images/dropdown-button.svg') 100% 100% no-repeat;
    margin-bottom: 2px;

}

.dropdown__options-wrapper {
    z-index: 10;
    position: absolute;
    display: flex;
    width: 200px;
    padding: 2px 0px;
    flex-direction: column;
    align-items: flex-start;
    gap: 1px;
    border-radius: 2px;
    background: var(--primary-primary700, #151B29);
    box-shadow: 0px 0px 6px 0px rgba(0, 0, 0, 0.75);
}

.dropdown__option {
    display: flex;
    width: 100%;
    padding: 6px 12px;
    justify-content: center;
    align-items: flex-start;
    gap: 10px;
    align-self: flex-start;
    background: var(--primary-primary500, #212B41);

    overflow: hidden;
    color: #FFF;
    text-overflow: ellipsis;
    white-space: nowrap;

    font-family: "Gotham Pro";
    font-size: 14px;
    font-style: normal;
    font-weight: 400;
    line-height: 20px;
    letter-spacing: 0.252px;
    cursor: pointer;
}

.dropdown__option-icon {
    width: 17px;
    height: 16px;
    background: url('../../images/option-icon.svg') 100% 100% no-repeat;
    background-color: transparent;
}

.dropdown__option-text {
    width: 100%;
}

.dropdown__option-pressed {
    border-left: 2px solid var(--secondary-secondary500);
    background: var(--primary-primary700, #151B29);
}

.dropdown__option-disabled {
    color: var(--gradients-grey, #868F98);
    opacity: 0.5;
    cursor: auto;
}

.dropdown__option:hover {
    background: var(--primary-primary600);

}

.slide-fade-enter-active {
    transition: all 0.3s ease-out;
}

.slide-fade-leave-active {
    transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
}

.slide-fade-enter-from,
.slide-fade-leave-to {
    transform: translateX(20px);
    opacity: 0;
}

.bottomRight {
  top: 107%;
  left: calc(100% - 24px);
}
.topRight {
  bottom: 107%;
  left: 0;
}
.bottomLeft {
  top: 107%;
  right: calc(100% - 24px);
}
.topLeft {
  bottom: 107%;
  right: calc(100% - 24px);
}
</style>