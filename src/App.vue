<script setup>
	import { RouterLink, RouterView } from "vue-router";
</script>

<template>
	<header>
		<div class="wrapper">
			<nav>
				<RouterLink to="/">Products</RouterLink>
				<RouterLink to="/product">Add Product</RouterLink>
			</nav>
		</div>
	</header>

	<RouterView />
</template>
