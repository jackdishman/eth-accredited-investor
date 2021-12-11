<script setup lang="ts">
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import { ref } from "Vue";

const searchValue = ref(``);

function search(): void {
	console.log(searchValue.value);
}
</script>

<template>
	<input
		type="text"
		v-model="searchValue"
		placeholder="Enter ETH address or .ens"
	/>
	<button @click="search">Search</button>
</template>

<style>
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
}
</style>
