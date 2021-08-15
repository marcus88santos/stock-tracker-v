<template>
	<div>
		<table>
			<TableHeader />
			<!-- <TableBody /> -->
		</table>
		<p v-if="!body">
			Please, insert a stock.
		</p>
	</div>
</template>

<script>
	import TableHeader from './TableHeader.vue'
	// import TableBody from './TableBody'
	import axios from 'axios'
	export default {
		name: 'Table',
		components: { TableHeader },
		data () {
			return {
				body: [],
			}
		},
		created () {
			axios.get('http://localhost:3000/stock').then(
				res => {
					this.body = res.data
				},
				err => console.log(err)
			)
		},
	}
</script>

<style scoped>
	p {
		color: red;
		padding-top: 20px;
		text-align: center;
	}
</style>
