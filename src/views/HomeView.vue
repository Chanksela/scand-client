<template>
	<main>
		<div v-if="Object.keys(data).length > 0" class="product-container">
			<ul v-for="item in data">
				<li class="product-box">
					<input
						type="checkbox"
						name="product"
						class="checkbox"
						:id="item.id"
					/>
					<div>{{ item.sku }}</div>
					<div>{{ item.name }}</div>
					<div>{{ item.price }}</div>
					<div>{{ item.parameters }}</div>
				</li>
			</ul>
		</div>
		<div v-else>Couldn't fetch data, please wait for some time...</div>
	</main>
</template>
<script>
	export default {
		data() {
			return {
				data: {},
			};
		},
		mounted() {
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
	};
</script>
<style scoped>
	.product-container {
		display: flex;
		flex-wrap: wrap;
		justify-content: flex-start;
		align-items: center;
		gap: 10px;
		padding: 0.6rem 1rem;
	}
	.product-box {
		width: 200px;
		height: 200px;
		border: 1px solid #ccc;
		padding: 5px;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		gap: 5px;
		position: relative;
	}
	.checkbox {
		position: absolute;
		top: 5px;
		left: 5px;
	}
</style>
