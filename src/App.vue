<template>
	<header>
		<Navigation
			:fetchData="fetchData"
			:selectedProducts="selectedProducts"
			@selectedProducts="handleSelectedProducts"
		/>
	</header>
	<main>
		<RouterView
			:data="data"
			:selectedProducts="selectedProducts"
			@selectedProducts="handleSelectedProducts"
		/>
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
				selectedProducts: [],
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
			// assigning the selected products to the selectedProducts array from HomeView.vue
			handleSelectedProducts(products) {
				this.selectedProducts = products;
			},
		},
		mounted() {
			this.fetchData();
		},
	};
</script>
