<script setup>
import ProductCard from "@/components/ProductCard.vue";
import Pagination from "@/components/Pagination.vue";
import {
	onBeforeMount,
	onBeforeUnmount,
	onBeforeUpdate,
	onMounted,
	onUnmounted,
	onUpdated,
	ref,
} from "vue";

// Lifecycle hook onBeforeMount dipanggil sebelum komponen dimount ke DOM.
// Digunakan untuk melakukan operasi asinkron yang perlu dilakukan sebelum komponen dirender.
// Di sini saya menggunakan setTimeout untuk menyalakan operasi asinkron dan mencetak pesan ke konsol.
onBeforeMount(async () => {
	await new Promise((resolve) => setTimeout(resolve, 1000)); // Tunggu 1 detik
	console.log("Komponen sedang dimount"); // Cetak pesan ke konsol
});

// Lifecycle hook onMounted dipanggil setelah komponen dimount ke DOM.
// Digunakan untuk melakukan operasi yang perlu dilakukan setelah komponen dirender.
// Di sini saya menggunakan setTimeout untuk mengundurkan waktu pencetakan pesan ke konsol.
onMounted(() => {
	setTimeout(() => {
		console.log("Komponen telah dimount"); // Cetak pesan ke konsol setelah 2 detik
	}, 2000);
});

// Lifecycle hook onBeforeUpdate dipanggil sebelum komponen diperbarui.
// Digunakan untuk melakukan operasi yang perlu dilakukan sebelum komponen dirender ulang.
// Di sini saya menggunakan setTimeout untuk menyalakan operasi asinkron dan mencetak pesan ke konsol.
onBeforeUpdate(async () => {
	await new Promise((resolve) => setTimeout(resolve, 1000)); // Tunggu 1 detik
	console.log("Komponen sedang diperbarui"); // Cetak pesan ke konsol
});

// Lifecycle hook onUpdated dipanggil setelah komponen diperbarui.
// Digunakan untuk melakukan operasi yang perlu dilakukan setelah komponen dirender ulang.
// Di sini saya menggunakan setTimeout untuk mengundurkan waktu pencetakan pesan ke konsol.
onUpdated(async () => {
	await new Promise((resolve) => setTimeout(resolve, 2000)); // Tunggu 2 detik
	console.log("Komponen telah diperbarui"); // Cetak pesan ke konsol setelah 2 detik
});

// Lifecycle hook onBeforeUnmount dipanggil sebelum komponen di-unmount dari DOM.
// Digunakan untuk melakukan operasi yang perlu dilakukan sebelum komponen dihapus.
// Di sini saya menggunakan setTimeout untuk menyalakan operasi asinkron dan mencetak pesan ke konsol.

const page = ref(1);

function nextPage() {
	page.value++;
}
</script>

<template>
	<main>
		{{ page }}
		<button @click="nextPage">Next</button>
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
