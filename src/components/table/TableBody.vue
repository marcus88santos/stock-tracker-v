<template>
	<tbody>
		<tr v-for="stock in stocks" :key="stock.index">
			<td>
				<span
					id="icon-remove"
					class="material-icons"
					@click="$emit('remove-stock', stock)"
				>
					close
				</span>
				<span
					id="icon-edit"
					class="material-icons"
					@click="$emit('edit-stock', stock)"
				>
					edit
				</span>
			</td>
			<td class="tbody__type">{{ stock.type }}</td>
			<td class="tbody__code">{{ stock.code }}</td>
			<td class="tbody__targetPriceTax">
				{{
					Intl.NumberFormat('pt-BR', {
						style: 'decimal',
						minimumFractionDigits: 2,
					}).format(stock.targetPriceTax)
				}}
			</td>
			<td v-show="stock.currentPriceTax" class="tbody__currentPriceTax">
				{{
					Intl.NumberFormat('pt-BR', {
						style: 'decimal',
						minimumFractionDigits: 2,
					}).format(stock.currentPriceTax)
				}}
			</td>
		</tr>
	</tbody>
</template>

<script>
	export default {
		name: 'TableBody',
		emits: ['edit-stock', 'remove-stock'],
		data () {
			return {}
		},
		props: ['stocks'],
	}
</script>

<style scoped>
	td {
		text-align: center;
		padding: 7px;
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
	#icon-remove {
		color: rgb(255, 80, 80);
		cursor: pointer;
		font-size: 20px;
		vertical-align: middle;
		padding-inline: 15px;
	}
	#icon-remove:hover {
		color: red;
	}
	#icon-edit {
		color: rgb(255, 255, 150);
		cursor: pointer;
		font-size: 15px;
		vertical-align: middle;
		padding-inline: 15px;
	}
	#icon-edit:hover {
		color: yellow;
	}
	tr {
		border-bottom: 1px solid rgb(30, 30, 30);
	}
</style>
