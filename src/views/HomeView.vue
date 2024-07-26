<script setup>
import ProductCard from "@/components/ProductCard.vue";
import Pagination from "@/components/Pagination.vue";

import { onMounted, ref, watch } from "vue";
import axios from "axios";

const products = ref([]);
const page = ref(1);
const limit = ref(8);
const API_URL = `http://localhost:3000/products?_page=${page.value}&_per_page=${limit.value}`;

// Await then to get data from API (Fastest)
onMounted(async () => {
	products.value = await axios.get(API_URL).then((res) => res.data);
});

// Async await to get data from API (Structured)
// async function getProducts() {
// 	const response = await axios.get("http://localhost:3000/products");
// 	products.value = response.data;
// 	console.log(response.data);
// }
// getProducts();

watch(page, async () => {
	products.value = await axios.get(API_URL).then((res) => res.data);
});

function changePage(newPage) {
	if (newPage < 1) return;
	if (newPage > products.value.pages) return;
	page.value = newPage;
}
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
			<Pagination
				:page="page"
				:totalPages="products.pages"
				@change-page="changePage"
			/>
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
