<template>
    <div v-for="card in productCards" :key='card.id' class="col-md-6">
		<div class="card mb-4" data-id="{{ card.id }}">
	        <img class="product-img" :src="card.img" alt="">
				<div class="card-body text-center">
					<h4 class="item-title">{{ card.title }}</h4>
					<p><small data-items-in-box class="text-muted">6 шт.</small></p>
						<div class="details-wrapper">
							<div class="items counter-wrapper">
								<div class="items__control" @click='reduceCounter(card.id)' data-action="minus">-</div>
    							<div class="items__current" data-counter>{{ card.count }}</div>
								<div class="items__control" @click='increaseCounter(card.id)' data-action="plus">+</div>
							</div>

					<div class="price">
								<div class="price__weight">{{ card.weight }}г.</div>
								<div class="price__currency">{{ card.price }} ₽</div>
				    </div>
				</div>
				<button @click='addInBasket(card.id)' data-cart type="button" class="btn btn-block btn-outline-warning">+ в корзину</button>							
            </div>
		</div>
	</div>
</template>

    

<script>
export default {
    name: 'vCard',
	props: {
        productCards: {
            type: Array,
            required: true,
        }
    },

	methods: {
		increaseCounter(cardID){
			this.productCards.forEach((el) => {
				if(el.id == cardID ){ 
					el.count += 1
				}
			})
    	},

		reduceCounter(cardID){
			this.productCards.forEach((el) => {
				if(el.id == cardID && el.count > 1){ 
					el.count -= 1
				}
			})
		},

		addInBasket(cardID){
      		this.productCards.forEach((el) => {
				if(el.id === cardID){
					let cardForBasket = {
						id: el.id,
						title: el.title,
						count: el.count,
						weight: el.weight,
						price: el.price,
						img: el.img
					}
					this.$emit('addInBasket', cardForBasket)
					el.count = 1
				}
				
      		})
    	},
	}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>