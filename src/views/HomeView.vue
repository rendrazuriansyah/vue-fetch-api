<script setup>
import ProductCard from "@/components/ProductCard.vue";
import Pagination from "@/components/Pagination.vue";
import { ref } from "vue";
</script>

<template>
	<main>
		<div class="product-grid">
			<ProductCard />
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
