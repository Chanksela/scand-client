<template>
	<header>
		<div class="wrapper">
			<h1>Product List</h1>
			<nav>
				<RouterLink to="/">Products</RouterLink>
				<RouterLink to="/product">Add Product</RouterLink>
			</nav>
		</div>
	</header>

	<RouterView />
</template>
<script setup>
	import { RouterLink, RouterView } from "vue-router";
</script>
