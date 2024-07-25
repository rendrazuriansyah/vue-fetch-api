<script setup>
import ProductCard from "@/components/ProductCard.vue";
import Pagination from "@/components/Pagination.vue";

import { ref, watch } from "vue";
import axios from "axios";

const products = ref([]);
const page = ref(1);
const limit = ref(8);

// Await then to get data from API (Fastest)
products.value = await axios
	.get(
		`http://localhost:3000/products?_page=${page.value}&_per_page=${limit.value}`
	)
	.then((res) => res.data);
console.log(products.value);

// Async await to get data from API (Structured)
// async function getProducts() {
// 	const response = await axios.get("http://localhost:3000/products");
// 	products.value = response.data;
// 	console.log(response.data);
// }
// getProducts();

watch(page, async () => {
	products.value = await axios
		.get(
			`http://localhost:3000/products?_page=${page.value}&_per_page=${limit.value}`
		)
		.then((res) => res.data);
});
</script>

<template>
	<main>
		<div class="product-grid">
			<ProductCard
				v-for="(product, index) in products.data"
				:key="index"
				:product="product"
			/>
		</div>
		<div class="pagination">
			<Pagination />
		</div>
	</main>
</template>

<style scoped>
.product-grid {
	display: grid;
	grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
	gap: 20px;
	width: 80%;
	margin: 0 auto;
}

.pagination {
	display: flex;
	justify-content: center;
	align-items: center;
	margin-top: 20px;
}
</style>
