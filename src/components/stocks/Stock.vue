<template>
	<div class="col-sm-6 col-md-4">
		<div class="card border-success">
			<div class="card-header text-success">
				<h3>
					{{ stock.name }}
					<small>(Price: {{ stock.price }})</small>
				</h3>
			</div>
			<div class="card-body">
				<div class="float-left">
					<input 
						type="number"
						class="form-control"
						placeholder="Quantity"
						v-model.number="quantity"
						:class="{ danger: insufficientFunds }"
						>
				</div>
				<div class="float-right">
					<button 
						class="btn btn-success"
						@click="buyStock"
						:disabled="insufficientFunds || quantity <= 0"
						>{{ insufficientFunds ? 'Not enough' : 'Buy' }}
					</button>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	export default {
		props: ['stock'],

		data() {
			return {
				quantity: 0
			}
		},

		computed: {

			funds() {
				return this.$store.getters.funds;
			}, 

			insufficientFunds() {
				return this.quantity * this.stock.price > this.funds;
			}
		},

		methods: {
			buyStock() {
				const order = {
					stockId: this.stock.id,
					stockPrice: this.stock.price,
					quantity: this.quantity
				};

				this.$store.dispatch('buyStock', order);
				this.quantity = 0;
			}
		}
	}
</script>

<style scoped>
	
	.card {

		margin: 30px 0px 0px 0px;
		padding: 20px;
	}

	.danger {
		border: 1px solid red;
	}
</style>