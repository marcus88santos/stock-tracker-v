<template>
	<div id="form">
		<select v-model="stock.type" id="type">
			<option value="" selected disabled>Tipo</option>
			<option value="acoes">Ações</option>
			<option value="fii">FII</option>
			<option value="tesouroDireto">Tesouro Direto</option>
		</select>
		<select
			v-model="stock.code"
			v-if="stock.type == 'tesouroDireto'"
			required
			id="stockT"
		>
			<option value="" selected disabled>Ativo</option>
			<option value="tdPre2026">TD Pré 2026</option>
			<option value="tdIpca+2026">TD IPCA+ 2026</option>
		</select>
		<input
			v-model="stock.code"
			v-else
			type="text"
			id="stock"
			placeholder="Ativo"
		/>
		<input
			v-model="stock.targetPriceTax"
			placeholder="Preço/Taxa alvo"
			type="number"
			step=".01"
			id="priceTax"
		/>
		<span id="icon-add" class="material-icons" @click="submit">
			done
		</span>
		<span id="icon-close" class="material-icons" @click="$emit('closeForm')">
			close
		</span>
	</div>
</template>
<script>
	export default {
		name: 'Form',
		emits: ['closeForm'],
		data () {
			return {
				stock: {
					type: '',
					code: '',
					targetPriceTax: '',
				},
			}
		},
		methods: {
			submit () {
				console.log(this.stock)
				this.stock = {
					type: '',
					code: '',
					targetPriceTax: '',
				}
			},
		},
	}
</script>
<style scoped>
	#form {
		align-items: center;
		background-color: rgb(150, 150, 150);
		display: flex;
		justify-content: center;
		padding: 7px 80px;
	}
	#icon-close {
		color: red;
		cursor: pointer;
		font-size: 30px;
		position: absolute;
		right: 80px;
	}
	#icon-add {
		cursor: pointer;
		margin-inline: 20px;
		font-size: 30px;
	}
	#icon-add:hover {
		color: rgb(0, 255, 0);
	}
	select {
		border: 1px solid #ccc;
		border-radius: 5px;
		cursor: pointer;
		font-size: 14px;
		height: 30px;
		margin-inline: 20px;
		outline: 0px;
		padding-inline: 3px;
		width: 130px;
	}
	select:focus {
		box-shadow: 0 0 4px 2px black;
	}
	input {
		border: 1px solid #ccc;
		border-radius: 5px;
		font-size: 14px;
		height: 30px;
		margin-inline: 20px;
		outline: 0px;
		padding-inline: 5px;
		width: 130px;
		text-align: center;
	}
	input:focus {
		box-shadow: 0 0 4px 2px black;
	}
	input:-webkit-autofill {
		-webkit-box-shadow: 0 0 0 30px white inset;
	}
	::placeholder {
		color: rgb(100, 100, 100);
	}
	select:invalid {
		color: rgb(100, 100, 100);
	}
	select option:first-child {
		color: rgb(100, 100, 100);
	}
	select:invalid option:not(:first-child) {
		color: black;
	}
	input[type='number'] {
		width: 130px;
		padding-inline: 2px;
	}
	input[type='number']::-webkit-inner-spin-button {
		height: 30px;
	}
</style>
