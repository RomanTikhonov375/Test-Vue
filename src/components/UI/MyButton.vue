<template>
    <button class="button"><slot></slot></button>
</template>

<script>
    export default {
        name: 'MyButton'
    }
</script>

<style scoped>
.button {
    padding: 5px;
    align-self: flex-end;
    margin-top: 15px;
    background-color: transparent;
    color: slategray;
    border: 1px solid slategray;
}
</style>
