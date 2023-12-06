<template>
	<header>
		<Navigation
			:fetchData="fetchData"
			:selectedProducts="selectedProducts"
			@selectedProducts="handleSelectedProducts"
			@saveHandler="saveHandler"
		/>
	</header>
	<main>
		<RouterView
			:fetchData="fetchData"
			:data="data"
			:selectedProducts="selectedProducts"
			:clicked="clicked"
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
				clicked: 0,
			};
		},
		methods: {
			fetchData() {
				try {
					fetch("http://scandi-api.000webhostapp.com/", {
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
			// handling the save button click
			saveHandler(value) {
				this.clicked = value;
			},
		},
		mounted() {
			this.fetchData();
		},
	};
</script>
