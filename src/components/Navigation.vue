<template>
	<div v-if="this.$route.name === 'home'">
		<h1>Product List</h1>
		<nav>
			<RouterLink to="/product">Add </RouterLink>
			<a href="#">Mass Delete</a>
		</nav>
	</div>
	<div v-else>
		<h1>Product Add</h1>
		<nav>
			<a>Save</a>
			<RouterLink to="/">Cancel</RouterLink>
		</nav>
	</div>
</template>
<script>
	import { RouterLink } from "vue-router";
	export default {
		components: {
			RouterLink,
		},
	};
</script>
