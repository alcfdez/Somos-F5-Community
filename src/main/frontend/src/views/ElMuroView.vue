<script setup>
import { ref , onBeforeMount } from 'vue';
import Header from '../components/Header.vue';
import UserFeed from '../components/UserFeed.vue';
import AddPublication from '../components/AddPublication.vue';

import PostService from '../services/PostService';
import CardProfile from '../components/CardProfile.vue';


const postService = new PostService();

let posts = ref([]);

onBeforeMount(async()=>{
	await postService.fetchAllPost()
	posts.value = postService.getPost()
	console.log(posts.value)
	});
</script>

<template>
<main>
<Header/>
<UserFeed/>
<div class="tools">
 
    
</div>
<div class="publi">
    <CardProfile
			v-for= "post in posts" :post="post"/>
</div>
</main>
</template>

<style lang="scss" scoped>
@use "@/scss/colors" as c;
main {
  margin: 0 auto;
  width: 80%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
.tools {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 90vw;
    .modal-container {
        align-self: start;
        .modal {
            background: map-get(c.$colors, "white");
            display: flex;
            border: 2px solid black;
            width: 100%;
            // padding: 2em;
            font-size: 1.2em;
            color: black;
            height: 2em;
            .btn-add {
                margin-left: 1em;
            }
        }
    }
}

.publi{
  margin-top: 2em;
}
}
</style>