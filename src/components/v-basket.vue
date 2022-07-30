<template>
  	<div class="cart-wrapper">
		<div v-if="this.basket.length > 0" v-for="card in basket" :key='card.id' class="cart-item" data-id="02">
			<div class="cart-item__top">
				<div class="cart-item__img">
					<img :src="card.img" alt="">
				</div>
				<div class="cart-item__desc">
    				<div class="cart-item__title">{{ card.title }}</div>
					<div class="cart-item__weight">6 шт. / {{ card.weight }}г.</div>
					<!-- cart-item__details -->
					<div class="cart-item__details">
						<div class="items items--small counter-wrapper">
							<div class="items__control" @click='basketReduceCounter(card.id)' data-action="minus">-</div>
							<div class="items__current" data-counter="">{{ card.count }}</div>
							<div class="items__control" @click='basketIncreaseCounter(card.id)' data-action="plus">+</div>
						</div>
                        <div class="price">
						    <div class="price__currency">{{ card.price }} ₽</div>
						</div>
        			</div>
					<!-- // cart-item__details -->
				</div>
			</div>
		</div>
        <div v-else data-cart-empty class="alert alert-secondary" role="alert">
            Корзина пуста
		</div>
	</div>
</template>

<script>
export default {
    name: 'vBasket',
	props: {
        basket: {
            type: Array,
            required: true,
        }
    },

	methods: {
		basketIncreaseCounter(cardID){
			this.basket.forEach((el) => {
				if(el.id == cardID ){ 
					el.count += 1
					this.$emit('priceCalc', el.price, '+')
				}
			})
		},

		basketReduceCounter(cardID){
			this.basket.forEach((el) => {
				if(el.id == cardID ){
					if(el.count >1 ){
						el.count -=1
					} else {
						this.basket.splice(this.basket.findIndex(a => a.id === cardID), 1)
					}
					this.$emit('priceCalc', el.price)
				}		
			})	
		}
	}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>