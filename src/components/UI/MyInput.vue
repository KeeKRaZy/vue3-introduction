<template>
        <input
            :value="modelValue"
            @input="updateInput"
            class="input" 
        >
</template>

<script>
export default{
    name: "my-input",
    props: {
        modelValue: [String, Number]
    },
    methods: {
        updateInput(event) {
            this.$emit('update:modelValue', event.target.value)
        }
    }
}
</script>

<style scoped>
.input{
    display: block;
    padding: 5px 10px;
    font-size: 14px;
    margin-top: 5px;
    border-radius: 2px;
}
</style>