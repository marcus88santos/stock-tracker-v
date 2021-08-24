<template>
	<div id="form">
		<select
			@change="this.stock.code = ''"
			required
			v-model="stock.type"
			id="type"
		>
			<option value="" selected disabled>Tipo</option>
			<option value="Ações">Ações</option>
			<option value="FII">FII</option>
			<option value="Tesouro Direto">Tesouro Direto</option>
		</select>
		<select
			v-model="stock.code"
			v-if="stock.type == 'Tesouro Direto'"
			id="stockT"
			required
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
			@input="numberFormat($event)"
		/>
		<span
			:class="{ valid: isValid }"
			id="icon-add"
			class="material-icons"
			@click="submit"
		>
			done
		</span>
		<span id="icon-close" class="material-icons" @click="$emit('close-form')">
			close
		</span>
	</div>
</template>

<script>
	import axios from 'axios'
	export default {
		name: 'Form',
		emits: ['close-form', 'force-update'],
		data () {
			return {
				stock: {
					id: this.edStock._id,
					type: this.edStock.type,
					code: this.edStock.code,
					targetPriceTax: this.edStock.targetPriceTax,
				},
				isValid: false,
			}
		},
		props: ['edStock'],
		methods: {
			submit () {
				if (this.stock.id) {
					//realizar update
				} else {
					axios.post('http://localhost:3000/stock', this.stock).then(
						() => {
							this.stock = {
								id: '',
								type: '',
								code: '',
								targetPriceTax: '',
							}
						},
						e => console.log(e)
					)
				}
				if (this.isActive()) {
					this.stock = {
						id: '',
						type: '',
						code: '',
						targetPriceTax: '',
					}
					this.$emit('close-form')
				}
				this.$emit('force-update')
			},
			isActive () {
				if (
					this.stock.type != '' &&
					this.stock.targetPriceTax != '' &&
					this.stock.targetPriceTax != ''
				) {
					return true
				}
				return false
			},
			numberFormat (event) {
				if (
					event.inputType == 'deleteContentBackward' ||
					event.inputType == 'deleteContentForward'
				) {
					this.stock.targetPriceTax = (0).toFixed(2)
				}
				if (event.target.value.length == 1 && event.data != null) {
					this.stock.targetPriceTax = (event.target.value / 100).toFixed(2)
				} else if (event.data != null) {
					this.stock.targetPriceTax = (
						this.stock.targetPriceTax * 10
					).toFixed(2)
				}
			},
		},
		created () {},
		watch: {
			'stock.type' () {
				this.isValid = this.isActive()
			},
			'stock.code' () {
				this.isValid = this.isActive()
			},
			'stock.targetPriceTax' () {
				this.isValid = this.isActive()
			},
			'edStock._id' () {
				this.stock = this.edStock
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
		color: rgb(255, 80, 80);
		cursor: pointer;
		font-size: 32px;
		position: absolute;
		right: 80px;
	}
	#icon-close:hover {
		color: red;
	}
	#icon-add {
		cursor: pointer;
		margin-inline: 20px;
		font-size: 30px;
	}
	.valid {
		color: lightgreen;
	}
	.valid:hover {
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
		color: black;
	}
	select:focus {
		box-shadow: 0 0 4px 2px black;
	}
	option {
		color: black;
	}
	option:first-child {
		color: rgb(100, 100, 100);
	}
	select:invalid {
		color: rgb(100, 100, 100);
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
		box-shadow: 0 0 0 30px white inset;
	}
	input[type='number'] {
		width: 130px;
		padding-inline: 2px;
	}
	input[type='number']::-webkit-inner-spin-button {
		height: 30px;
	}
</style>
