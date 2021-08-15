<template>
	<Header @open-form="formOn" />
	<Form v-if="formStatus" @close-form="formOff" />
</template>

<script>
	import Header from './components/header/Header.vue'
	import Form from './components/form/Form.vue'
	export default {
		name: 'App',
		components: { Header, Form },
		data () {
			return {
				formStatus: false,
			}
		},
		methods: {
			formOn () {
				this.formStatus = true
			},
			formOff () {
				this.formStatus = false
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
