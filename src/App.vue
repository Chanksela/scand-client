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
					fetch("https://scandiphp-api-7c4216600634.herokuapp.com/product", {
						method: "GET",
					})
						.then((response) => response.json())
						.then((data) => {
							this.data = data["products"];
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
