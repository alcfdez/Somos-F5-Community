<script setup>
	import { ref, onBeforeMount } from "vue";
	import { useProgrammatic } from "@oruga-ui/oruga-next";
	import InfoUser from "../components/InfoUser.vue";
	import Header from "../components/Header.vue";
	import AddPublication from "../components/AddPublication.vue";
	import ProfileService from "../services/ProfileService";
	import { useAuthStore } from "../stores/AuthStore";
 	import CardProfile from "../components/CardProfile.vue";
	const store = useAuthStore()

	let input = ref("");

	
	const profileService = new ProfileService();


	const postService = new PostService();


	let profile = ref();


 	onBeforeMount(async()=>{
	await profileService.fetchOneProfile(store.id)
	profile.value = profileService.getProfile()
	console.log(profile.value)
});

// function filteredList() {
// 	return posts.value.filter((post) =>
// 		post.title.toLowerCase().includes(input.value.toLowerCase())||
// 		post.description.toLowerCase().includes(input.value.toLowerCase())
// 		// ||profile.name.toLowerCase().includes(input.value.toLowerCase())
// 	);
// }

	onBeforeMount(async () => {
		await postService.fetchAllPost();
		posts.value = postService.getPost();
		console.log(posts.value);
	});

	function filteredList() {
		return posts.value.filter(
			post =>
				post.title
					.toLowerCase()
					.includes(input.value.toLowerCase()) ||
				post.description
					.toLowerCase()
					.includes(input.value.toLowerCase())
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
		<Header />
		<InfoUser />
		<div class="title">
			<div class="text">
				<h2>Mis publicaciones</h2>
			</div>
			<img
				class="star"
				src="https://uploads-ssl.webflow.com/62e2b7b9c42bdda27c83d493/6329c1bcb276576e8a46f894_shape-2.svg"
				alt="Imagen de una estrella color lila."
			/>
		</div>
		<section class="modal-container">
			<o-button
				@click="cardModal()"
				class="modal"
			>
				AÑADIR PUBLICACION
				<i class="fa-solid fa-plus btn-add"></i>
			</o-button>
			<div class="input-search">
				<i
					class="lupa fa-solid fa-magnifying-glass"
					style="color: #adadad"
				></i>
				<input
					type="text"
					v-model="input"
					placeholder="Buscar publicaciones..."
				/>
			</div>
		</section>

		

			<CardProfile
			v-for= "post in profile.posts" :post="post"/>
		


		<CardProfile
			v-for="post in filteredList()"
			:post="post"
		/>

		<div
			class="itemError"
			v-if="input && !filteredList().length"
		>
			<p>No results found!</p>
		</div>

	</main>
</template>

<style lang="scss" scoped>
	@use "@/scss/colors" as c;
	@use "@/scss/fonts";

	.title {
		width: 46vw;
		display: flex;
		align-items: center;
		justify-content: center;
		margin-top: 1em;

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
		width: 80%;
		display: flex;
		justify-content: center;
		align-items: center;
		flex-direction: column;
	}

	.modal-container {
		align-self: start;
		display: flex;
		justify-content: space-between;
		width: 100%;

		.input-search{
			display:flex;
			background-color: map-get(c.$colors, "light-purple");
			border-radius: 5px;
			align-items: center;
			height: 2.8em;
			width: 20vw;

			i{
				font-size: 1.1em;
				margin: .3em;
			}
		}

		input {
			outline: none;
		}

		.modal {
			border-radius: 5px;
			background: map-get(c.$colors, "white");
			margin-bottom: 10vh;
			display: flex;
			border: 2px solid black;
			width: 20vw;
			font-size: 1.2em;
			color: black;
			height: 2em;

			.btn-add {
				margin-left: 1em;
			}
		}
	}

	@media (max-width: 599px) {
		.title {
			width: 80%;
			display: flex;
			align-items: center;
			justify-content: center;
			.text {
				font-size: 1.2rem;
			}

			.star {
				width: 12%;
				right: 7%;
			}
		}
		.modal-container {
			margin-top: 2%;
			width: 60%;
			font-size: 50%;
		}
	}
</style>

