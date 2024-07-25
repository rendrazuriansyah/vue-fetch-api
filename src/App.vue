<script setup>
import { RouterLink, RouterView } from "vue-router";
import HomeView from "./views/HomeView.vue";
</script>

<template>
	<!-- <RouterView /> -->
	<Suspense>
		<template #default>
			<HomeView />
		</template>
		<template #fallback>
			<p>Loading...</p>
		</template>
	</Suspense>
</template>

<style scoped></style>
