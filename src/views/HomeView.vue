<template>
	<main>
		<div v-if="Object.keys(data).length > 0" class="product-container">
			<ul v-for="item in data" :key="item.id">
				<li class="product-box">
					<input
						class="checkbox"
						type="checkbox"
						name="product"
						:value="item.id"
						v-model="selectedProducts"
					/>
					<div>{{ item.sku }}</div>
					<div>{{ item.name }}</div>
					<div>{{ item.price }}</div>
					<div>{{ item.parameters }} {{ measurementUnit(item.type_id) }}</div>
				</li>
			</ul>
		</div>
		<div v-else class="product-container">
			Couldn't fetch data, please wait for some time...
		</div>
	</main>
</template>

<script>
	export default {
		props: {
			data: {
				type: Object,
				required: true,
			},
		},
		emits: ["selected-products"],
		data() {
			return {
				selectedProducts: [],
			};
		},
		methods: {
			// emitting the selected products to the parent component
			emitSelectedProducts() {
				this.$emit("selected-products", this.selectedProducts);
			},
			measurementUnit(type) {
				return type == 1 ? "MB" : type == 2 ? "KG" : "";
			},
		},

		watch: {
			selectedProducts: {
				handler() {
					this.emitSelectedProducts();
				},
				deep: true,
			},
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
		border: 1px solid #10132c;
		box-shadow: 3px 2px 5px #10132c;
		padding: 5px;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		text-align: center;
		gap: 5px;
		position: relative;
		cursor: default;
	}
	.product-box:hover {
		border: 1px solid #e04f4f;
		box-shadow: 3px 2px 5px #e04f4f;
		font-size: 1.025rem;
		transition: 0.3s ease-in;
	}
	.checkbox {
		position: absolute;
		top: 15px;
		left: 15px;
	}
</style>
