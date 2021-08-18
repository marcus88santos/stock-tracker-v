<template>
	<div>
		<div id="header">
			<img :src="logo" :alt="appName" id="logo" />
			<h1>{{ appName }}</h1>
			<span id="icon-add" class="material-icons" @click="$emit('openForm')">
				add
			</span>
		</div>
		<div class="updated">
			<p>
				Delay: 15 min. Last update:
				<!-- <span>{{ lastUpdate }} </span> -->
			</p>
		</div>
	</div>
</template>
<script>
	export default {
		name: 'Header',
		emits: ['openForm'],
		data () {
			return {
				logo: '/img/logo.png',
				appName: 'Stock Tracker V',
				add: '/img/add.svg',
			}
		},
		methods: {},
		// props: {
		// 	lastUpdate,
		// },
	}
</script>
<style scoped>
	#header {
		align-items: center;
		background-color: rgb(50, 50, 50);
		display: flex;
		justify-content: space-between;
		padding: 10px 75px;
	}
	#logo {
		height: 40px;
		width: 40px;
	}
	h1 {
		color: white;
		font-size: 25px;
	}
	#icon-add {
		color: lightgreen;
		display: block;
		font-size: 40px;
		transition: 0.2s;
		cursor: pointer;
	}
	#icon-add:hover {
		color: rgb(0, 255, 0);
	}
	.updated {
		background-color: rgb(100, 100, 100);
		padding: 5px;
		text-align: center;
	}
	.updated p {
		font-size: 0.8em;
	}
</style>
