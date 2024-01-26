<template>
    <div class="checkbox-wrapper" v-if="checkbox.visible">
        <input v-bind:value="checkbox.id" type="checkbox" v-bind:id="checkbox.id" required class="my-checkbox"
            v-bind:disabled="checkbox.disabled" @change="updateInput()">
        <label class="checkbox-label" v-bind:for="checkbox.id">
            {{ checkbox.title }} <slot></slot>
        </label>
    </div>
</template>

<script>

export default {
    name: 'MyCheckbox',
    props: {
        checkbox: {
            type: Object,
            required: true,
        },

    },
    data() {
        return {

            checkboxNewList: []
        }
    },
    methods: {
        updateInput() {
            this.$emit('renderlist', this.checkboxNewList)
        }
    }
}
</script>

<style scoped>
.checkbox-wrapper {
    margin-top: 20px;
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
    /* 133.333% */
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