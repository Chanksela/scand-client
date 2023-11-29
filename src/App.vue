<template>
	<header>
		<Navigation />
	</header>
	<main>
		<RouterView />
	</main>
	<footer><Footer /></footer>
</template>
<script>
	import Navigation from "./components/Navigation.vue";
	import { RouterView } from "vue-router";
	import Footer from "./components/Footer.vue";
	export default {
		components: {
			Navigation,
			RouterView,
			Footer,
		},
	};
</script>
