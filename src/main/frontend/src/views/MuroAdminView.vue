<script setup>
	import { ref, onBeforeMount } from "vue";
	import { useProgrammatic } from "@oruga-ui/oruga-next";
import HeaderAdmin from '../components/HeaderAdmin.vue';
import BannerAdmin from '../components/BannerAdmin.vue';
import PostService from "../services/PostService";
import CardProfile from "../components/CardProfile.vue";
import AddPublication from "../components/AddPublication.vue"

const trapFocus = ref(false);
	const { oruga } = useProgrammatic();

	function cardModal() {
		oruga.modal.open({
			component: AddPublication,
			trapFocus: true,
		});
	}



import ProfileService from '../services/ProfileService';


const profileService = new ProfileService();
	
	let profiles = ref([]);
 	onBeforeMount(async()=>{
	await postService.fetchAllPost()
	await profileService.fetchAllProfiles();
	posts.value = postService.getPost()
	console.log(posts.value.idProfile);
	console.log(posts.profile_id);
	profiles.value = profileService.getProfile();
	console.log(profiles.value);
	console.log(posts.value)
	});


let input = ref("");

const postService = new PostService();

let posts = ref([]);

onBeforeMount(async () => {
  await postService.fetchAllPost();
  posts.value = postService.getPost();
  console.log(posts.value);
});

function filteredList() {
  return posts.value.filter(
    (post) =>
      post.title.toLowerCase().includes(input.value.toLowerCase()) ||
      post.description.toLowerCase().includes(input.value.toLowerCase())
  );
}

const trapFocus = ref(false);
const { oruga } = useProgrammatic();

function cardModal() {
  oruga.modal.open({
    component: AddPublication,
    trapFocus: true,
  });
}






</script>

<template>
<main>
<HeaderAdmin/>
<BannerAdmin/>
<section class=" modal-container">
			<o-button
				@click="cardModal()"
				class="modal"
			>
				AÑADIR PUBLICACION
				<i class="fa-solid fa-plus btn-add"></i>
			</o-button>
		</section>
<Search/>

			<CardProfile
			v-for= "post in posts" :post="post"/>

</main>

</template>

<style lang="scss">
@use "@/scss/colors" as c;
@use "@/scss/fonts";

main{
  margin: 0 auto;
  width: 80%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

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
</style>




