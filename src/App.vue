<template>
	<header>
		<Navigation :fetchData="fetchData" />
	</header>
	<main>
		<RouterView :data="data" />
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
		data() {
			return {
				data: {},
			};
		},
		methods: {
			fetchData() {
				try {
					fetch("http://localhost:8000", {
						method: "GET",
					})
						.then((response) => response.json())
						.then((json) => {
							this.data = json["products"];
						});
				} catch (error) {
					console.error("An error occurred:", error);
				}
			},
		},
		mounted() {
			this.fetchData();
		},
	};
</script>
