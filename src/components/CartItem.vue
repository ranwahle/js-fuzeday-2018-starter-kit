<template>
	<div class="cart-item">
		<img class="image" v-bind:src="image">
		<div class="text">
			<div class="title">{{ data.title }}</div>
			<div class="vendor">{{ data.vendor }}</div>
			<div class="description">{{ data.description }}</div>
			<div class="price">{{ price }}$</div>

			<div class="actions">
				<div class="quantity-text">Quantity: {{rangeValue}}</div>
				<mt-range
					v-model="rangeValue"
					:min="0"
					:max="10"
					:step="1"
					:bar-height="1"
					class="item-quantity"
				>
					<div slot="start" class="range-number">0</div>
					<div slot="end" class="range-number">10</div>
				</mt-range>
				<mt-button type="danger" size="small" plain @click="$store.dispatch('remove', data.id)">Remove</mt-button>
			</div>
		</div>
	</div>
</template>

<script>
	import { Button, Range } from 'mint-ui';

	export default {
		name: 'CartItem',
		props: {
			data: Object
		},
		data() {
			return {
				rangeValue: this.data.qty
			}
		},
		computed: {
			image() {
				return this.data.images[0].src;
			},
			price() {
				return parseFloat(this.data.variants[0].price) * this.data.qty ;
			}
		},
		components: {
			Button,
		  	Range
		}
	}
</script>

<style scoped lang="scss">
	.cart-item {
		margin: 1em 0;
		padding: 1em;
		display: flex;
		border-radius: 4px;
		border: 1px solid #DDD;

		&:hover {
		}

		.image {
			min-width: 200px;
			height: 200px;
		}

		.text {
			padding: 0 10px;
			position: relative;
		}

		.title {
			font-size: 16px;
			font-weight: bold;
			display: block;
		}

		.vendor {
			font-size: 10px;
			font-weight: lighter;
			font-style: italic;
			padding-bottom: 10px;
			display: block;
		}

		.description {
			font-size: 12px;
			font-weight: lighter;
			display: block;
			padding-bottom: 10px;
		}

		.price {

		}

		.actions {
			position: absolute;
			bottom: 0;
			right: 0;
			display: block;
			text-align: right;

			.mint-button {
				display: inline-block;
				&:hover{
					background: #ef4f4f;
					color: white;
				}
			}

			.quantity-text {
				display: inline-block;
				font-size: 12px;
			}

			.item-quantity {
				width: 150px;
				display: inline-flex;
				padding-right: 10px;

				.range-number {
					font-size: 10px;
					padding: 0 10px;
					opacity: .3;
				}
			}
		}
	}
</style>