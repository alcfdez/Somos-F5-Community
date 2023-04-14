<script setup>
import Header from '../components/Header.vue';
import UserContacts from '../components/UserContacts.vue';
import CardUsers from '../components/CardUsers.vue';
</script>

<template>
    <main>
<Header/>
<UserContacts/>
<CardUsers/>
</main>
</template>

<style lang="scss" scoped>
@use "@/scss/colors" as c;
@use "@/scss/fonts";
main {
    width: 100%;
}

</style>