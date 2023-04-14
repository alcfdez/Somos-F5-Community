<script setup>
	import { ref, onBeforeMount } from "vue";
	import { useProgrammatic } from "@oruga-ui/oruga-next";
	import InfoUser from "../components/InfoUser.vue";
	import CardProfile from "../components/CardProfile.vue";
	import Header from "../components/Header.vue";
	import AddPublication from "../components/AddPublication.vue";
	import PostService from "../services/PostService";
	
	
	const postService = new PostService();
	let posts = ref([]);
 	onBeforeMount(async()=>{
	await postService.fetchAllPost()
	posts.value = postService.getPost()
	console.log(posts.value)
	});



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
		<Header/>
		<InfoUser />

		<div class="title">
			
				<h2 class="text">Mis publicaciones</h2>
		

			<img
				class="star"
				src="https://uploads-ssl.webflow.com/62e2b7b9c42bdda27c83d493/6329c1bcb276576e8a46f894_shape-2.svg"
				alt="Imagen de una estrella color lila."
			/>
		</div>
		<section class=" modal-container">
			
			<o-button
				@click="cardModal()"
				class="modal"
			>
				AÑADIR PUBLICACION
				<i class="fa-solid fa-plus btn-add"></i>
			</o-button>
		</section>
			<CardProfile
			v-for= "post in posts" :post="post"/>

		
	</main>
</template>

<style lang="scss" scoped>
	@use "@/scss/colors" as c;
	@use "@/scss/fonts";

	.title {
		// width: 46vw;
		// display: flex;
		// align-items: center;
		// justify-content: center;
		// margin-top: 1em;

		.text {
			font-size: xx-large;
			color: map-get(c.$colors, "black");
			font-family: "Open Sans", sans-serif;
			font-weight: bold;
			z-index: 1;
		}

		.star {
			position: relative;
			width: 5%;
			right: 3%;
		}
	}

	main {
		margin: 0 auto;
		width: 100%;
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
