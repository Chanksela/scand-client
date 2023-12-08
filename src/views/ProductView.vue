<template>
	<div class="container">
		<form id="product_form" @submit="handleSubmit" ref="productForm">
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
						step="0.01"
						placeholder="Product Price"
						required
					/>
				</div>
			</section>
			<section class="form-section">
				<div class="input-wrapper">
					<label for="productType">Type Switcher</label>
					<select name="productType" id="productType" v-model="productType">
						<option :value="1">DVD</option>
						<option :value="2">Book</option>
						<option :value="3">Furniture</option>
					</select>
				</div>
			</section>
			<section class="form-section">
				<div class="optional-section" id="DVD" v-if="productType == 1">
					<div class="input-wrapper">
						<label for="size">Size (MB)</label>
						<input
							type="number"
							id="size"
							name="size"
							step="0.01"
							placeholder="Size in MB"
							required
						/>
					</div>
					<p class="product-description">Please enter the size of DVD in MB</p>
				</div>
				<div class="optional-section" id="Book" v-else-if="productType == 2">
					<div class="input-wrapper">
						<label for="weight">Weight (KG)</label>
						<input
							type="number"
							id="weight"
							name="weight"
							step="0.01"
							placeholder="Weight in KG"
							required
						/>
					</div>
					<p class="product-description">Please enter the book in KG</p>
				</div>
				<div
					class="optional-section"
					id="Furniture"
					v-else-if="productType == 3"
				>
					<div class="input-wrapper">
						<label for="height">Height (CM)</label>
						<input
							type="number"
							id="height"
							name="height"
							step="0.01"
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
							step="0.01"
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
							step="0.01"
							placeholder="Length in CM"
							required
						/>
					</div>
					<p class="product-description">
						Please enter dimensions of Furniture in HxWxL
					</p>
				</div>
			</section>
			<button type="submit" ref="submitButton" hidden />
		</form>
		<div class="error-container">
			<div class="error" v-if="errors">
				{{ errors.error }}
			</div>
		</div>
	</div>
</template>
<script>
	export default {
		data() {
			return {
				productType: 1,
				errors: {},
			};
		},
		props: {
			// receiving the clicked value from the parent component
			clicked: {
				type: Number,
				required: true,
			},
			// accepting fetchData function to refresh the products list after save action
			fetchData: {
				type: Function,
				required: true,
			},
		},
		methods: {
			handleSubmit(e) {
				e.preventDefault();
				const formData = new FormData(e.target);
				const data = Object.fromEntries(formData);
				fetch("https://scandiphp-api-7c4216600634.herokuapp.com/product", {
					method: "POST",
					headers: {
						"Content-Type": "application/json",
					},
					mode: "cors",
					body: JSON.stringify(data),
				})
					.then((response) => {
						if (response.ok) {
							this.clearFormInputs();
							this.fetchData();
							this.$router.push("/");
						} else {
							return response.json();
						}
					})
					.then((data) => {
						const sessionData = data.sessionData;
						this.errors = sessionData;
						console.log(sessionData);
					})
					.catch((error) => {
						console.log(error);
					});
			},
			clearFormInputs() {
				this.$refs.productForm.reset();
				this.productType = 1;
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
	.container {
		height: 100%;
		display: flex;
	}
	.error-container {
		display: flex;
		justify-content: center;
		height: 100%;
		margin-top: 10rem;
		font-size: larger;
		font-weight: bold;
		color: red;
	}
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
	input,
	input::placeholder {
		text-indent: 5px;
	}
	input,
	select {
		padding: 0.6rem;
		width: 15rem;
	}
	input {
		border-radius: 3px;
		outline: none;
		border: none;
	}
	label {
		font-weight: 600;
	}
</style>
