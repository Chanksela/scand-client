<template>
	<header>
		<Navigation />
	</header>
	<RouterView />
</template>
<script>
	import { RouterView } from "vue-router";
	import Navigation from "./components/Navigation.vue";
	export default {
		components: {
			Navigation,
			RouterView,
		},
	};
</script>
