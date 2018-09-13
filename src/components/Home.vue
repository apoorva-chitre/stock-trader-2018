<template>
	<div class="container">
		<h1>Trade or View your Portfolio</h1>
		<br>
		<h6>You may Save & Load your Data</h6>
		<h6>Click on 'End Day' to begin a New Day!</h6>
		<hr>
		<p class="lead">You Funds: {{ funds | currency }}</p>
	</div>
</template>

<script>
	export default {
		computed: {
			funds() {
				return this.$store.getters.funds;
			}
		}
	}
</script>

<style scoped>
	
	.container {
		margin: 30px 0px 0px 0px;
	}

	.lead {

		font-weight: bold;
		background-color: #C0C0C0;
		color: #000;
		padding: 10px;
		text-align: center;
	}

</style>	