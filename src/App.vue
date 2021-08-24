<template>
	<Header @open-form="formOn" />
	<Form
		v-if="formStatus"
		@close-form="formOff"
		:edStock="stock"
		@force-update="forceUpdate"
	/>
	<Table @edit-stock="formOn($event)" :forceUpdate="update" />
</template>

<script>
	import Header from './components/header/Header.vue'
	import Form from './components/form/Form.vue'
	import Table from './components/table/Table.vue'
	export default {
		name: 'App',
		emits: ['edit-stock'],
		components: { Header, Form, Table },
		data () {
			return {
				formStatus: false,
				stock: {
					_id: '',
					type: '',
					code: '',
					targetPriceTax: '',
				},
				update: 0,
			}
		},
		methods: {
			formOn (stock) {
				this.formStatus = true
				if (stock) {
					this.stock = stock
				}
			},
			formOff () {
				this.stock = {
					_id: '',
					type: '',
					code: '',
					targetPriceTax: '',
				}
				this.formStatus = false
			},
			forceUpdate () {
				this.update += 1
			},
		},
	}
</script>

<style>
	* {
		font-family: Arial, Helvetica, sans-serif;
		margin: 0;
		padding: 0;
		box-sizing: border-box;
	}
</style>
