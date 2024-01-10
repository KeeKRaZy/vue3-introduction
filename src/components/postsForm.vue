<template>
    <form>
        <p>New post</p>
        <my-input 
            v-model="post.title"
            @input="post.title = $event.target.value" 
            type="text" 
            placeholder="Title"
        ></my-input>
        <my-input 
            v-model="post.body" 
            @input="post.body = $event.target.value" 
            type="text" 
            placeholder="Discirption"
        ></my-input>
        <my-input 
            v-model="post.number"
            @keyup="back2back()" 
            @input="post.number = $event.target.value" 
        ></my-input>
        <my-button 
            @click="createPost()" 
            type="button"
        >Post
        </my-button>
        <my-button 
        style="display: inline;"
            @click="plusnumber()" 
            type="button"
        >+
        </my-button>
        <my-button 
            style="display: inline; margin-left: 10px;"
            @click="minusnumber()" 
            type="button"
        >-
        </my-button>
    </form>

</template>

<script>

export default{
    data() {
        return {
            post: {
                title: '',
                body: '',
                number: 0,
            }
        }
    },
    props: {
        number: Number
    },
    watch: { 
        number: function() { 
            this.post.number = this.number;
        }
    },
    methods: {
        createPost(){
            this.post.id = Date.now();
            this.$emit('create', this.post)
            this.post = {
                title: '',
                body: '',
                number: 0,
            }
        },
        plusnumber(){
            this.$emit('plus')
        },
        minusnumber(){
            this.$emit('minus')
        },
        back2back(){
            this.$emit('inputchanges', this.post.number)
        }
    }
}

</script>

<style scoped>
form{
    margin-top: 20px;
}

form p{
    font-weight: bold;
    font-size: 20px;
}
form input, form button{
    display: block;
    padding: 5px 10px;
    font-size: 14px;
    margin-top: 5px;
}
</style>