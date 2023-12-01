<script></script>
<template>
	<main>
		<form action="" id="product-form">
			<section class="product-main-input">
				<div class="input-wrapper">
					<label for="sku">SKU</label>
					<input
						type="text"
						id="sku"
						name="sku"
						placeholder="Please enter the SKU"
						required
					/>
				</div>
				<div class="input-wrapper">
					<label for="name">Name</label>
					<input
						type="text"
						id="name"
						name="name"
						placeholder="Please enter the name of the product"
						required
					/>
				</div>
				<div class="input-wrapper">
					<label for="price">Price ($)</label>
					<input
						type="number"
						id="price"
						name="price"
						placeholder="Please enter the price of the Product"
						required
					/>
				</div>
			</section>
			<section class="product-switcher">
				<div class="input-wrapper">
					<label for="productType">Type Switcher</label>
					<select name="productType" id="productType" v-model="productType">
						<option value="DVD">DVD</option>
						<option value="Furniture">Furniture</option>
						<option value="Book">Book</option>
					</select>
				</div>
			</section>
			<section
				class="product-optional-input"
				id="DVD"
				v-if="productType === 'DVD'"
			>
				<p>Please enter the size of DVD in MB</p>
				<div class="input-wrapper">
					<label for="size">Size (MB)</label>
					<input
						type="number"
						id="size"
						name="size"
						placeholder="Size of dvd in MB"
						required
					/>
				</div>
			</section>
			<section
				class="product-optional-input"
				id="Furniture"
				v-else-if="productType === 'Furniture'"
			>
				<p>Please enter dimensions of Furniture in HxWxL</p>
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
			</section>
			<section
				class="product-optional-input"
				id="Book"
				v-else-if="productType === 'Book'"
			>
				<p>Please enter the book in KG</p>
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
			</section>
		</form>
	</main>
</template>
<script>
	export default {
		data() {
			return {
				productType: "DVD",
			};
		},
	};
</script>
