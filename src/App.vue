<template>
    <div class="app">
        <my-input
            class="searchPosts"
            placeholder="Search by title..."
            v-model="searchPosts"
        />
        <h3>Post list</h3>
        <my-select 
            class="sortSelect"
            v-model="sortSelect"
            :options="options"
        />
        <all-posts
            class="allPosts"
            :posts="sortedAndSearchedPosts"
            @deletePost="deletePost"
            v-if="!loadingStatus" 
        />
        <my-button 
        v-if="!loadingStatus" 
        @click="this.popupStatus = true;"
        >Create new post</my-button>
        <h1 v-else>Posts are loading...</h1>
        <my-popup v-model:show="popupStatus">        
            <post-form
                @create="createPost"
                @inputchanges="inputchanges"
                :number="number"
                @plus="plusnumber"
                @minus="minusnumber"
            />
        </my-popup>
    </div>
</template>

<script>
import allPosts from "@/components/allPosts.vue";
import postRating from "@/components/postsRating.vue";
import postForm from "@/components/postsForm.vue";
import axios from 'axios';

export default{
    components: {
        allPosts, postRating, postForm
    },

    data() {
        return {
            number: 0,
            posts: [
                {id: 64431312, title: 'Animals', body: 'Animals are dying ', number: 4},
                {id: 31251, title: 'Cars', body: 'What is common between cars and', number: 2},
                {id: 908907, title: 'Females', body: 'Everyone love females', number: 5},
            ],
            popupStatus: false,
            loadingStatus: false,
            sortSelect: '',
            searchPosts: '',
            options: [
                {value: 'title', name: 'Title'},
                {value: 'body', name: 'Discription'},
            ]
        }
    },
    computed: {
        sortedPosts() {
            return [...this.posts].sort((post1, post2) => {
                return post1[this.sortSelect]?.localeCompare(post2[this.sortSelect])
            })
        },
        sortedAndSearchedPosts(){
            return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchPosts.toLowerCase()))
        }
    },
/*  watch: { 
        sortSelect(newVal) { 
            this.posts.sort((post1, post2) => {
                return post1[newVal]?.localeCompare(post2[newVal])
            })
        }
    },  */
    methods: {
        createPost(post){
            this.posts.push(post);
            this.popupStatus = false;
        },
        plusnumber(){
            this.number += 1;
        },
        minusnumber(){
            if(this.number > 0){
                this.number -= 1;
            }
        },
        inputchanges(changednumber){
            this.number = parseInt(changednumber);
        },
        deletePost(post){
            this.posts = this.posts.filter(onepost => onepost.id != post.id);
        },
        async fetchposts(){
            try {
                this.loadingStatus = true;
                setTimeout(async () =>{
                    const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=3');
                    response.data.forEach((post) => {
                        post["number"] = Math.floor(Math.random() * 9);
                        this.posts.push(post)
                    });
                    this.loadingStatus = false;
                }, 1000)
            } catch (e) {
                alert('server error')
            }
        }
    },
    mounted(){
        this.fetchposts();
    }
}
</script>

<style scoped>
*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.app{
    padding: 20px;
}
.sortSelect{
    position: absolute;
    right: 30px;
    margin-top: -23px;
}
.searchPosts{
    width: 100%;
    margin-bottom: 10px;
}
h1{
    margin-top: 30px;
}
</style>