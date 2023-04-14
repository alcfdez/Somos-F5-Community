<script setup>
import Header from '../components/Header.vue';
import UserFeed from '../components/UserFeed.vue';
import AddPublication from '../components/AddPublication.vue';
import Search from '../components/Search.vue'
import PostComp from '../components/PostComponent.vue'

</script>

<template>
    <main>
    <Header/>
<UserFeed/>

   
    <Search/>


    <PostComp/>

</main>
</template>

<style lang="scss" scoped>
@use "@/scss/colors" as c;

main {
    margin: 0 auto;
    width: 1000px;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;

}


</style>