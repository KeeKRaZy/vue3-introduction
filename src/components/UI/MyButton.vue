<template>
        <button type="button" class="btn">
            <slot></slot>
        </button>
</template>

<script>
export default{
    name: "my-button"
}
</script>

<style scoped>
.btn{
    padding: 3px 10px;
    font-size: 15px;
    background-color: rgba(255, 255, 255, 1);
    border: 1px solid grey;
    cursor: pointer;
}
.btn:hover{
    background-color: rgba(212, 212, 212, 0.4);
}
</style>