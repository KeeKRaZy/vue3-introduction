<template>

    <div class="container" v-if="posts.length > 0">
        <transition-group name="post-list">
            <one-post 
                v-for="post in posts"
                :post="post"
                :key="post.id"
                @deletePost="$emit('deletePost', post)"
            />
        </transition-group>

    </div>
    <div v-else>
        <h2>No posts yet</h2>
    </div>

</template>

<script>
import onePost from "@/components/onePost";
export default{
    components: {onePost},
    props: {
        posts:{
            type: Array,
            required: true
        }
        
    },
    methods: {
        deletePost(post){
            this.$emit('deletePost', post);
        }
    }
}
</script>

<style scoped>
.container{
    margin-top: 10px;
}
.post-list-item {
  display: inline-block;
  margin-right: 10px;
}
.post-list-enter-active, .post-list-leave-active {
  transition: all 0.5s ease;
}
.post-list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
.post-list-enter-from{
  opacity: 0;
  transform: translateX(-30px);
}
.post-list-move{
    transition: all 0.5s ease;
}
</style>