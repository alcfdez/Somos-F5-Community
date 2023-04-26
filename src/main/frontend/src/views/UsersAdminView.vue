<script setup>
import { ref, onBeforeMount } from "vue";
import HeaderAdmin from "../components/HeaderAdmin.vue";
import BannerAdmin from "../components/BannerAdmin.vue";
import UserService from "../services/UserService";
import CardUsers from "../components/CardUsers.vue";
import ProfileService from "../services/ProfileService";

const userService = new UserService();
const profileService = new ProfileService();
let users = ref([]);
let user = ref("");
let profile = ref([]);
onBeforeMount(async () => {
  await userService.fetchAllUsers();
  // user = userService.getUser();
  await profileService.fetchAllProfiles();
  profile.value = profileService.getProfile();
  users.value = userService.getUser();
  console.log(users);
  console.log(profile.value);
});

let input = ref("");

function filteredList() {
  return profile.value.filter(
    (profile) =>
      profile.name.toLowerCase().includes(input.value.toLowerCase()) ||
      profile.surname.toLowerCase().includes(input.value.toLowerCase()) ||
      profile.location.toLowerCase().includes(input.value.toLowerCase())
  );
}
</script>

<template>
  <main>
    <HeaderAdmin />
    <BannerAdmin />

    <div class="searcher">
      <div class="inputSearch">
        <i class="lupa fa-solid fa-magnifying-glass" style="color: #adadad"></i>
        <input type="text" v-model="input" placeholder="  Buscar usuarios..." />
      </div>
      <div class="itemError" v-if="input && !filteredList().length">
        <p>No results found!</p>
	</div>
</div>
<CardUsers
  v-for="user in filteredList()"
  :user="user"
  :profile="profile"
/>
  </main>
</template>

<style lang="scss">
@use "@/scss/colors" as c;
@use "@/scss/fonts";

main {
  margin: 0 auto;
  width: 80%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.searcher {
	margin-top: 2em;
    background-color: map-get(c.$colors, "light-purple");
    width: 30vw;
    height: 2.5em;
    border-radius: 3px;
    
    
    .inputSearch {
      display: flex;
      flex-direction: row;
      justify-content: center;
      align-items: center;
      width: 100%;
      font-family: "OpenSans";
      font-size: 1.5vw;
      margin-bottom: 5vh;
      padding-left: 1%;
      
      .lupa {
        font-size: 1em;
      }
      
      input {
        outline: none;
        width: 100%;
      }
      
      }
    
	}
    .itemError {
      font-family: "OpenSans";
      font-size: 2vw;
    }

</style>
