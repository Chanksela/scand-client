<template>
	<div v-if="this.$route.name === 'home'" class="nav-container">
		<h1 class="nav-header">Product List</h1>
		<nav class="nav-links">
			<RouterLink to="/product" class="btn-link">Add </RouterLink>
			<a href="#" class="btn-link" @click="handleDelete">Mass Delete</a>
		</nav>
	</div>
	<div v-else class="nav-container">
		<h1 class="nav-header">Product Add</h1>
		<nav class="nav-links">
			<a class="btn-link" @click="emitSaveHandler">Save</a>
			<RouterLink to="/" class="btn-link">Cancel</RouterLink>
		</nav>
	</div>
</template>
<script>
	import { RouterLink } from "vue-router";
	export default {
		components: {
			RouterLink,
		},
		props: {
			// receiving the fetchData function from the parent component
			fetchData: {
				type: Function,
				required: true,
			},
			// receiving the selected products from the parent component
			selectedProducts: {
				type: Array,
				required: true,
			},
		},
		emits: ["save-handler"],
		data() {
			return {
				clicked: 0,
			};
		},
		methods: {
			handleDelete() {
				fetch("https://scandiphp-api-7c4216600634.herokuapp.com/product", {
					method: "DELETE",
					headers: {
						"Content-Type": "application/json",
					},
					mode: "cors",
					credentials: "include",
					body: JSON.stringify({
						// sending the selected products to the backend
						ids: this.selectedProducts,
					}),
				})
					.then((response) => {
						// refreshing the products list after delete action
						this.fetchData();
					})
					.catch((error) => {
						console.log(error);
					});
			},
			// emitting the clicked value to the parent component
			emitSaveHandler() {
				this.clicked++;
				this.$emit("save-handler", this.clicked);
			},
		},
	};
</script>
<style scoped>
	.nav-container {
		display: flex;
		justify-content: space-between;
		align-items: center;
	}
	.nav-header {
		width: 80%;
		cursor: default;
		color: #10132c;
	}

	.nav-links {
		flex-grow: 1;
		display: flex;
		justify-content: flex-end;
		align-items: center;
		gap: 1rem;
	}
</style>
