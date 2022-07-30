<template>

  <v-header />
  
	<div class="container mb-5">
		<div class="row">
			<div class="col-md-8">
				<div class="row">

					<!-- Ролл -->
					<v-card 
          :productCards='productCards'
          @addInBasket='addInBasket'
          />
					<!-- // Ролл -->

				</div>
			</div>
			<div class="col-md-4">

				<!-- Корзина -->
				  <div class="card mb-4">
					<div class="card-body">
						<h4 class="card-title">Ваш заказ</h4>

						<!-- cart-wrapper -->
              <v-basket 
              :basket='basket'
              @priceCalc='priceCalc'
              />
						<!-- // cart-wrapper -->

						<!-- Стоимость заказа -->
						<div class="cart-total">
							<p v-if="this.finalPrice >= 1000"><span class="h5">Доставка:</span> <span class="delivery-cost free">бесплатно</span> </p>
							<p><span class="h5">Итого:</span> <span class="total-price">{{finalPrice}}</span> <span class="rouble">₽</span></p>
						</div>
						<!-- // Стоимость заказа -->

					</div>

					<!-- Оформить заказ -->
					<div v-if="this.basket.length > 0" id="order-form" class="card-body border-top">
						<h4 class="card-title">Оформить заказ</h4>
						<form>
							<div class="form-group">
								<input type="text" class="form-control" placeholder="Ваш номер телефона">
							</div>
							<button type="submit" class="btn btn-primary">Заказать</button>
						</form>
					</div>
					<!-- // Оформить заказ -->

				</div>
				<!-- // Корзина -->


			</div>
		</div>
	</div>

</template>

<script>
import vHeader from './components/v-header.vue'
import vCard from './components/v-card.vue'
import vBasket from './components/v-basket.vue'

export default {
  name: 'App',
  components: {
    vHeader, vCard, vBasket
  },
  data(){
    return {
      productCards: [
        { id: 1, img: 'img/roll/philadelphia.jpg', title: 'Филадельфия хит ролл', weight: '180', count: 1, price: '300' },
        { id: 2, img: 'img/roll/california-tempura.jpg', title: 'Калифорния темпура', weight: '205', count: 1, price: '250' },
        { id: 3, img: 'img/roll/zapech-california.jpg', title: 'Запеченый ролл «Калифорния»', weight: '182', count: 1, price: '230' },
        { id: 4, img: 'img/roll/philadelphia.jpg', title: 'Филадельфия', weight: '230', count: 1, price: '320' },
      ],

      basket: [],

      finalPrice: 0,
    }
  },

  methods: {

    addInBasket(objForBasket){
      this.finalPrice += objForBasket.count * objForBasket.price

      let cardInBasket = this.basket.find(el => el.id === objForBasket.id)
      if(cardInBasket) {
        this.basket.forEach((el) => {
          if(el.id == objForBasket.id) {
            el.count += objForBasket.count
          }
        })
      } 
    	else {
      	this.basket.push(objForBasket)
      }
    },

    priceCalc(price, sign){
      if (sign == '+') { 
          this.finalPrice += parseInt(price) 
      } else { 
        this.finalPrice -= price 
      }
    },

  }
  
}
</script>

<style>

</style>
