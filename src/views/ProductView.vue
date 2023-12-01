<script></script>
<template>
	<main>
		<form action="" id="product-form">
			<section class="product-main-input">
				<div class="input-wrapper">
					<label for="sku">SKU</label>
					<input type="text" id="sku" name="sku" required />
				</div>
				<div class="input-wrapper">
					<label for="name">Name</label>
					<input type="text" id="name" name="name" required />
				</div>
				<div class="input-wrapper">
					<label for="price">Price</label>
					<input type="number" id="price" name="price" required />
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
				<div class="input-wrapper">
					<label for="size">Size (MB)</label>
					<input type="number" id="size" name="size" required />
				</div>
			</section>
			<section
				class="product-optional-input"
				id="Furniture"
				v-else-if="productType === 'Furniture'"
			>
				<div class="input-wrapper">
					<label for="height">Height (CM)</label>
					<input type="number" id="height" name="height" required />
				</div>
				<div class="input-wrapper">
					<label for="width">Width (CM)</label>
					<input type="number" id="width" name="width" required />
				</div>
				<div class="input-wrapper">
					<label for="length">Length (CM)</label>
					<input type="number" id="length" name="length" required />
				</div>
			</section>
			<section
				class="product-optional-input"
				id="Book"
				v-else-if="productType === 'Book'"
			>
				<div class="input-wrapper">
					<label for="weight">Weight (KG)</label>
					<input type="number" id="weight" name="weight" required />
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
