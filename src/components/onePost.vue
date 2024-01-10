<template>
    <div class="fullPost">
        <div class="post">
            <div>
                <div><strong>Title:</strong> {{post.title}}</div>
                <div><strong>Discription:</strong> {{post.body}}</div>
                <div><strong>Number:</strong> {{post.number}}</div>
            </div>
            <div class="post-buttons">
                <my-button 
                @click="$emit('deletePost', this.post);"
            >X</my-button>
            </div>
        </div>
        <post-rating 
            :like="like" 
            :dislike="dislike"
            @addLike="addLike"
            @addDislike="addDislike"
        />
    </div>


</template>

<script>
import postRating from "@/components/postsRating";
export default{
    components: {postRating},
    props: {
        post:{
            type: Object,
            required: true
        }
        
    },
    data() {
        return {
            like: 0,
            dislike: 1,
        }
    },
    methods: {
        addLike(){
            this.like += 1;
        },
        addDislike(){
            this.dislike += 1;
        },
    }
}
</script>

<style scoped>
.post{
    display: flex;
    justify-content: space-between;
}
.fullPost{
    background-color: rgb(255, 244, 230);
    border: 1px solid black;
    padding: 10px;
    margin: 10px 0px;

}
.post div div{
    margin-top: 5px;
}
.post-buttons{
    margin-left: 10px;
}

</style>