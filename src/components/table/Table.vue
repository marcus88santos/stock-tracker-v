<template>
	<div>
		<table>
			<TableHeader />
			<TableBody
				:stocks="stocks"
				@edit-stock="$emit('edit-stock', $event)"
				@remove-stock="removeStock($event)"
			/>
		</table>
		<p v-if="stocks.length == 0">
			Please, insert a stock.
		</p>
	</div>
</template>

<script>
	import TableHeader from './TableHeader.vue'
	import TableBody from './TableBody'
	import axios from 'axios'
	export default {
		name: 'Table',
		emits: ['edit-stock', 'remove-stock'],
		components: { TableHeader, TableBody },
		data () {
			return {
				stocks: [],
			}
		},
		created () {
			this.update()
		},
		methods: {
			removeStock (event) {
				axios.delete(`http://localhost:3000/stock/${event._id}`).then(
					() => this.update(),
					e => console.log(e)
				)
			},
			update () {
				axios.get('http://localhost:3000/stock').then(
					res => {
						this.stocks = res.data.stocks
					},
					err => console.log(err)
				)
			},
		},
		props: ['forceUpdate'],
		watch: {
			forceUpdate () {
				console.log('update')
				this.update()
			},
		},
	}
</script>

<style scoped>
	p {
		color: red;
		padding-top: 20px;
		text-align: center;
	}
	table {
		background-color: rgb(40, 40, 40);
		width: 100%;
		border-collapse: collapse;
	}
</style>
