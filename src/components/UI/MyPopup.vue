<template>
    <div class="blackout" v-if="show" @click="this.$emit('update:show', false)">
        <div @click.stop class="popup">
            <slot></slot>
        </div>
    </div>
</template>

<script>
export default{
    name: "my-popup",
    props: {
        show: {
            type: Boolean,
            default: false,
        }
    }
}
</script>

<style scoped>
.blackout{
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    display: flex;
    position: fixed;
    background-color: rgba(0,0,0, 0.8);
}
.popup{
    margin: auto;
    background-color: white;
    min-height: 100px;
    min-width: 300px;
    padding: 20px;
}
</style>