<template>
	<tr>
		<th>
			<span id="icon-settings" class="material-icons">
				settings
			</span>
		</th>
		<th :style="cssVars" v-for="titulo in cabecalho" :key="titulo.index">
			{{ titulo }}
		</th>
	</tr>
</template>

<script>
	export default {
		name: 'TableHeader',
		data () {
			return {
				cabecalho: ['Tipo', 'Ativo', 'Preço/Taxa alvo', 'Preço/Taxa atual'],
				celWidth: {
					type: Number,
				},
			}
		},
		created () {
			this.celWidth = 100 / (this.cabecalho.length + 1)
		},
		computed: {
			cssVars () {
				return {
					'--width': this.celWidth + '%',
				}
			},
		},
	}
</script>

<style scoped>
	tr {
		border-bottom: 1px solid whitesmoke;
	}
	th {
		color: white;
		padding: 7px;
		font-size: 13px;
		width: var(--width);
	}
	#icon-settings {
		font-size: 15px;
		vertical-align: bottom;
	}
</style>
