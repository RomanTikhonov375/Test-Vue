<template>
    <div class="dropdown__wrapper" ref="dropDown">

        <div class="dropdown__selected-option" @click="isDropDownVisible = true">
        </div>
        <Transition name="slide-fade">
            <div class="dropdown__options-wrapper" v-if="isDropDownVisible">
                <div class="dropdown__option" v-for="(option, index) in props.options" :key="index"
                    @click="toggleOptionSelect(option)">
                    {{ option.name || option }}
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
const emit = defineEmits(['update:modelValue'])


const toggleOptionSelect = (option) => {
    selecredOption.value = option
    emit('update:modelValue', option)
    isDropDownVisible.value = false
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

onMounted(() => {
    window.addEventListener('click', onCloseDropDown)
})

onBeforeUnmount(() => {
    window.removeEventListener('click', onCloseDropDown)
})


</script>

<style scoped>
.dropdown__wrapper {
    width: 200px;
}

.dropdown__selected-option {
    cursor: pointer;
    width: 24px;
    height: 24px;
    background: url('../../images/dropdown-button.svg') 100% 100% no-repeat;
    margin-bottom: 2px;
}

.dropdown__options-wrapper {
    display: flex;
    width: 200px;
    padding: 2px 0px;
    flex-direction: column;
    align-items: flex-start;
    gap: 1px;
    border-radius: 2px;
    background: #151B29;
    /* dropdown shadow */
    box-shadow: 0px 0px 6px 0px rgba(0, 0, 0, 0.75);
}

.dropdown__option {
    display: flex;
    padding: 6px 12px;
    flex-direction: column;
    justify-content: center;
    align-items: flex-start;
    gap: 10px;
    align-self: stretch;
    background: #212B41;

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
}

.dropdown__option:hover {
    background-color: transparent;
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
</style>