<template>
	<tr v-for="stock in stocks" :key="stock.index">
		<td></td>
		<td class="tbody__type">{{ stock.type }}</td>
		<td class="tbody__code">{{ stock.code }}</td>
		<td class="tbody__targetPriceTax">{{ stock.targetPriceTax }}</td>
		<td class="tbody__currentPriceTax"></td>
	</tr>
</template>

<script>
	export default {
		name: 'TableBody',
		data () {
			return {}
		},
		props: ['stocks'],
	}
</script>

<style scoped>
	td {
		text-align: center;
		padding: 10px;
	}
	.tbody__type {
		color: white;
	}
	.tbody__code {
		color: white;
	}
	.tbody__targetPriceTax {
		color: white;
	}
</style>
