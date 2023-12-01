<script></script>
<template>
	<form id="product_form" @submit="handleSubmit">
		<section class="form-section">
			<div class="input-wrapper">
				<label for="sku">SKU</label>
				<input
					type="text"
					id="sku"
					name="sku"
					placeholder="Product SKU"
					required
				/>
			</div>
			<div class="input-wrapper">
				<label for="name">Name</label>
				<input
					type="text"
					id="name"
					name="name"
					placeholder="Product Name"
					required
				/>
			</div>
			<div class="input-wrapper">
				<label for="price">Price ($)</label>
				<input
					type="number"
					id="price"
					name="price"
					placeholder="Product Price"
					required
				/>
			</div>
		</section>
		<section class="form-section">
			<div class="input-wrapper">
				<label for="productType">Type Switcher</label>
				<select name="productType" id="productType" v-model="productType">
					<option value="DVD">DVD</option>
					<option value="Furniture">Furniture</option>
					<option value="Book">Book</option>
				</select>
			</div>
		</section>
		<section class="form-section">
			<div class="optional-section" id="DVD" v-if="productType === 'DVD'">
				<div class="input-wrapper">
					<label for="size">Size (MB)</label>
					<input
						type="number"
						id="size"
						name="size"
						placeholder="Size in MB"
						required
					/>
				</div>
				<p class="product-description">Please enter the size of DVD in MB</p>
			</div>
			<div
				class="optional-section"
				id="Furniture"
				v-else-if="productType === 'Furniture'"
			>
				<div class="input-wrapper">
					<label for="height">Height (CM)</label>
					<input
						type="number"
						id="height"
						name="height"
						placeholder="Height in CM"
						required
					/>
				</div>
				<div class="input-wrapper">
					<label for="width">Width (CM)</label>
					<input
						type="number"
						id="width"
						name="width"
						placeholder="Width in CM"
						required
					/>
				</div>
				<div class="input-wrapper">
					<label for="length">Length (CM)</label>
					<input
						type="number"
						id="length"
						name="length"
						placeholder="Length in CM"
						required
					/>
				</div>
				<p class="product-description">
					Please enter dimensions of Furniture in HxWxL
				</p>
			</div>
			<div
				class="optional-section"
				id="Book"
				v-else-if="productType === 'Book'"
			>
				<div class="input-wrapper">
					<label for="weight">Weight (KG)</label>
					<input
						type="number"
						id="weight"
						name="weight"
						placeholder="Weight in KG"
						required
					/>
				</div>
				<p class="product-description">Please enter the book in KG</p>
			</div>
		</section>
		<button type="submit" ref="submitButton" hidden />
	</form>
</template>
<script>
	export default {
		data() {
			return {
				productType: "DVD",
			};
		},
		props: {
			// receiving the clicked value from the parent component
			clicked: {
				type: Number,
				required: true,
			},
		},
		methods: {
			handleSubmit(e) {
				e.preventDefault();
				const formData = new FormData(e.target);
				const data = Object.fromEntries(formData);
				console.log(data);
			},
		},
		watch: {
			// watching the clicked value for changes
			// when it changes, the submit button is clicked
			// and we try to submit the form
			clicked: {
				handler() {
					this.$refs.submitButton.click();
				},
				deep: true,
			},
		},
	};
</script>
<style scoped>
	#product_form {
		margin: 0.3rem 1rem;
		display: flex;
		flex-direction: column;
		justify-content: flex-start;
		align-items: flex-start;
		height: 100%;
		width: 60%;
		gap: 2%;
	}
	.form-section {
		height: 30%;
		width: 50%;
		display: flex;
		flex-direction: column;
	}

	.form-section:nth-child(1) {
		margin-top: 1rem;
		gap: 4rem;
	}
	.form-section:nth-child(2) {
		height: 20%;
		justify-content: flex-start;
		margin-top: 1rem;
	}
	.form-section:nth-child(3) {
		flex-grow: 1;
		justify-content: flex-start;
	}

	.input-wrapper {
		display: flex !important;
		justify-content: space-between;
		align-items: center;
		width: 100%;
	}
	.optional-section {
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		align-items: flex-start;
		gap: 4rem;
	}

	.product-description {
		margin-top: 0.2rem;
		color: #10132c;
	}
</style>
