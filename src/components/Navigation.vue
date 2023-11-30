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
			<a href="#" class="btn-link">Save</a>
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
			fetchData: {
				type: Function,
				required: true,
			},
			selectedProducts: {
				type: Array,
				required: true,
			},
		},
		methods: {
			handleDelete() {
				fetch("http://localhost:8000/product", {
					method: "DELETE",
					headers: {
						"Content-Type": "application/json",
					},
					body: JSON.stringify({
						ids: this.selectedProducts,
					}),
				})
					.then((response) => {
						this.fetchData();
					})
					.catch((error) => {
						console.log(error);
					});
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
	}

	.nav-links {
		flex-grow: 1;
		display: flex;
		justify-content: flex-end;
		align-items: center;
		gap: 1rem;
	}
</style>
