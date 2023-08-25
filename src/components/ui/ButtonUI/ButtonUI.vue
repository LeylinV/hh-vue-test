<template>
    <button @click="handleClick">
        <slot></slot>
    </button>
</template>

<script>
export default {
    methods: {
        handleClick() {
            this.$emit('click');
        }
    }
}
</script>

<style scoped>
button {
    display: flex;
    align-items: center;
    justify-content: center;
    border: 3px #01A7FD solid;
    border-radius: 100px;
    font-family: 'Cairo', sans-serif;
    background-color: transparent;
    cursor: pointer;
    color: #01A7FD;
    padding: 7px 28px;
    font-size: 18px;
}
</style>
