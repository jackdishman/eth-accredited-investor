<script setup lang="ts">
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import { ref } from "vue";
import { inject } from "vue";

const searchValue = ref(``);
const axios: any = inject(`axios`);
const apiKey = `8YAJ4YEIYUFABUU26S8N6UVM457QFNYYET`;

const balance = ref(0);

function search(): void {
	const address = searchValue.value;
	if (address === ``) {
		return;
	}
	// Fetch
	const getBalance =
		`https://api.etherscan.io/api?module=account&action=balance&address=` +
		address +
		`&tag=latest&apikey=` +
		apiKey;
	axios({
		method: `get`,
		url: getBalance,
	}).then((res: any) => {
		if (res.data.status === `0`) {
			alert(`invalid address`);
		}
		if (res.data.status === `1`) {
			console.log(res.data.result);
			balance.value = res.data.result;
		}
	});
}
</script>

<template>
	<input
		type="text"
		v-model="searchValue"
		placeholder="Enter ETH address or .ens"
	/>
	<button @click="search" @keyup.enter="search">Search</button>
	<h1 class="text-lg text-green-500">
		{{
			(Math.round((balance / 1000000000000000000) * 10000) / 10000).toFixed(4)
		}}
		ETH
	</h1>
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
