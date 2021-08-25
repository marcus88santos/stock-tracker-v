<template>
	<footer id="footer">
		<h3>Stock Tracker V &copy; 2021</h3>
		<div>
			<p>Contact me:</p>
			<ul>
				<li>
					<a
						target="_blank"
						href="http://www.linkedin.com/in/marcus88santos"
					>
						<img :src="linkedin" alt="linkedin" />
					</a>
				</li>
				<li>
					<a target="_blank" href="http://www.github.com/marcus88santos">
						<img :src="github" alt="github" />
					</a>
				</li>
			</ul>
		</div>
	</footer>
</template>

<script>
	export default {
		data () {
			return {
				linkedin: '/img/linkedin.png',
				github: '/img/github.png',
			}
		},
	}
</script>

<style scoped>
	#footer {
		align-items: center;
		background-color: rgb(60, 60, 60);
		bottom: 0;
		color: white;
		display: flex;
		height: 60px;
		justify-content: space-between;
		width: 100%;
	}
	p {
		padding: 5px;
		font-size: 12px;
	}
	div {
		align-items: center;
		display: flex;
	}
	ul {
		display: flex;
		list-style-type: none;
		padding-right: 25px;
	}
	li {
		padding-inline: 5px;
	}
	h3 {
		font-size: 14px;
		padding-left: 25px;
	}
	img {
		height: 20px;
	}
</style>
