<template>
    
    <div class="rating">
        <div>
            <my-button 
                class="button" 
                @click="addLike()"
            >Likes: <strong>{{ like }}</strong></my-button>
            <my-button 
                class="button" 
                @click="addDislike()"
            >Dislike: <strong>{{ dislike }}</strong></my-button>
        </div>
    </div>

</template>

<script>
export default{
    props: {
        like: Number,
        dislike: Number
    },
    methods: {
        addLike(){
            this.$emit('addLike')
        },
        addDislike(){
            this.$emit('addDislike')
        }
    },
}
</script>

<style scoped>
.rating{
    margin-top: 10px;
    font-size: 16px;
    display: block;
}
.rating div{
    display: block;
}

.button{
    margin-right: 5px;
}
</style>