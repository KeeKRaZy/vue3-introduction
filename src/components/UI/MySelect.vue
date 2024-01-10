<template>
    <div>
        <select @change="changeOption">
            <option selected disabled 
                value="" 
                >Sort by</option>
            <option
                v-for="option in options"
                :key="option.value"
                :value="option.value"
            >{{ option.name }}
            </option>
        </select>
    </div>
</template>

<script>
    export default {
        name: 'my-select',
        props: {
            modelValue :{
                type:  String
            },
            options: {
                type: Array,
                deafult: () => []
            }
        },
        methods: {
            changeOption(event){
                this.$emit('update:modelValue', event.target.value);
            }
        }

    }
</script>

<style scoped>
    select{
        cursor: pointer;
        color: black;
        padding: 2px;
        font-weight: bold;
    }
</style>