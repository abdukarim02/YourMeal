<template>
  <section class="main">
    <div class="main__content container">
      <div class="categories">
        <div class="categories__content">
          <button v-for="category in categories" :key="category.name" 
                  @click="filterCategory(category.name)"
                  :class="['categories__content-btn', { active: selectedCategory === category.name }]">
            <img :src="category.img" :alt="category.name" class="categories__btn-img">
            <span class="categories__btn-name">{{ category.name }}</span>
          </button>
        </div>
      </div>   
      <div class="card">
        <div class="card__content">
          <div class="card__content-header">
            <h5 class="card__header-name">Корзина</h5>
            <span class="card__header-number">{{ cart.length }}</span>
          </div>

          <div v-if="cart.length">
            <div class="card__content-basket">
              <div v-for="item in cart" :key="item.id" class="card__basket-body">
          <div class="card__body-bg">
            <img :src="item.img" alt="">
          </div>
          <div class="card__body-info">
            <h5 class="card__info-name">{{ item.name }}</h5>
            <span class="card__info-gram">{{ item.weight }}г</span>
            <p class="card__info-price">{{ item.price }}₽</p>
          </div>
          <div class="card__body-button">
            <button @click="decreaseQuantity(item)">-</button>
            <span class="card__button-number">{{ item.quantity }}</span>
            <button @click="increaseQuantity(item)">+</button>
          </div>
              </div>
            </div>

            <div class="card__content-footer">
              <div class="card__footer-total">
                <h5 class="card__total-name">Итого</h5>
                <span class="card__total-price">{{ totalPrice }}₽</span>
              </div>
              <button class="card__footer-btn">Оформить заказ</button>
            </div>
          </div>

          <div v-else class="card__empty">
            <p>Тут пока пусто :(</p>
          </div>
         </div>
      </div>   
      <div class="product">
        <div class="product__wrap">
          <div v-for="product in filteredProducts" :key="product.id" class="product__wrap-flex">
            <div class="product__flex-bg">
              <img :src="product.img" :alt="product.name" class="product__bg-img">
            </div>
            <div class="product__flex-info">
              <p class="product__info-price">{{ product.price }}₽</p>
              <p class="product__info-name">{{ product.name }}</p>
              <p class="product__info-gram">{{ product.weight }}г</p>
            </div>
            <button class="product__flex-btn" @click="addToCart(product)">Добавить</button>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
<script>
export default {
  data() {
    return {
      selectedCategory: 'Бургеры',
      categories: [
        { name: 'Бургеры', img: '/public/filter-1.png' },
        { name: 'Закуски', img: '/public/filter-2.png' },
        { name: 'Хот-доги', img: '/public/filter-3.png' },
        { name: 'Комбо', img: '/public/filter-4.png' },
        { name: 'Шаурма', img: '/public/filter-5.png' },
        { name: 'Пицца', img: '/public/filter-6.png' },
        { name: 'Вок', img: '/public/filter-7.png' },
        { name: 'Десерты', img: '/public/filter-8.png' },
        { name: 'Соусы', img: '/public/filter-9.png' },
      ],
      products: [
        { id: 1, name: 'Мясная бомба', category: 'Бургеры', img: '/public/product-1.png', price: 689, weight: 512 },
        { id: 2, name: 'Супер сырный', category: 'Бургеры', img: '/public/product-2.png', price: 550, weight: 520 },
        { id: 3, name: 'Сытный', category: 'Бургеры', img: '/public/product-3.png', price: 639, weight: 512 },
        { id: 4, name: 'Тяжелый удар', category: 'Бургеры', img: '/public/product-4.png', price: 480, weight: 520 },
        { id: 5, name: 'Вечная классика', category: 'Бургеры', img: '/public/product-5.png', price: 450, weight: 512 },
        { id: 6, name: 'Итальянский', category: 'Бургеры', img: '/public/product-6.png', price: 560, weight: 520 },
        { id: 7, name: 'Начос', category: 'Закуски', img: '/public/product-7.png', price: 250, weight: 220 },
        { id: 8, name: 'Картошка фри', category: 'Закуски', img: '/public/product-8.png', price: 245, weight: 180 },
        { id: 9, name: 'Луковые кольца', category: 'Закуски', img: '/public/product-9.png', price: 230, weight: 160 },
        { id: 10, name: 'Домашний хот-дог', category: 'Хот-доги', img: '/public/product-10.png', price: 290, weight: 220 },
        { id: 11, name: 'Жгучий хот-дог', category: 'Хот-доги', img: '/public/product-11.png', price: 239, weight: 180 },
        { id: 12, name: 'Классический хот-дог', category: 'Хот-доги', img: '/public/product-12.png', price: 220, weight: 160 },
        { id: 13, name: 'Мясная бомба', category: 'Комбо', img: '/public/product-1.png', price: 689, weight: 512 },
        { id: 14, name: 'Супер сырный', category: 'Комбо', img: '/public/product-2.png', price: 550, weight: 520 },
        { id: 15, name: 'Сытный', category: 'Комбо', img: '/public/product-3.png', price: 639, weight: 512 },
        { id: 16, name: 'Тяжелый удар', category: 'Шаурма', img: '/public/product-4.png', price: 480, weight: 520 },
        { id: 17, name: 'Вечная классика', category: 'Шаурма', img: '/public/product-5.png', price: 450, weight: 512 },
        { id: 18, name: 'Итальянский', category: 'Шаурма', img: '/public/product-6.png', price: 560, weight: 520 },
        { id: 19, name: 'Начос', category: 'Пицца', img: '/public/product-7.png', price: 250, weight: 220 },
        { id: 20, name: 'Картошка фри', category: 'Пицца', img: '/public/product-8.png', price: 245, weight: 180 },
        { id: 21, name: 'Луковые кольца', category: 'Пицца', img: '/public/product-9.png', price: 230, weight: 160 },
        { id: 19, name: 'Начос', category: 'Вок', img: '/public/product-10.png', price: 250, weight: 220 },
        { id: 20, name: 'Картошка фри', category: 'Вок', img: '/public/product-11.png', price: 245, weight: 180 },
        { id: 21, name: 'Луковые кольца', category: 'Вок', img: '/public/product-12.png', price: 230, weight: 160 },
        { id: 19, name: 'Начос', category: 'Десерты', img: '/public/product-1.png', price: 250, weight: 220 },
        { id: 20, name: 'Картошка фри', category: 'Десерты', img: '/public/product-2.png', price: 245, weight: 180 },
        { id: 21, name: 'Луковые кольца', category: 'Десерты', img: '/public/product-3.png', price: 230, weight: 160 },
        { id: 19, name: 'Начос', category: 'Соусы', img: '/public/product-4.png', price: 250, weight: 220 },
        { id: 20, name: 'Картошка фри', category: 'Соусы', img: '/public/product-5.png', price: 245, weight: 180 },
        { id: 21, name: 'Луковые кольца', category: 'Соусы', img: '/public/product-6.png', price: 230, weight: 160 },
      ],
      cart: []
    };
  },
  computed: {
    filteredProducts() {
      return this.products.filter(product => product.category === this.selectedCategory);
    },
    totalPrice() {
      return this.cart.reduce((sum, item) => sum + item.price * item.quantity, 0);
    }
  },
  methods: {
    filterCategory(category) {
      this.selectedCategory = category;
    },
    addToCart(product) {
      const item = this.cart.find(p => p.id === product.id);
      if (item) {
        item.quantity++;
      } else {
        this.cart.push({ ...product, quantity: 1 });
      }
    },
    increaseQuantity(item) {
      item.quantity++;
    },
    decreaseQuantity(item) {
      if (item.quantity > 1) {
        item.quantity--;
      } else {
        this.cart = this.cart.filter(p => p.id !== item.id);
      }
    }
  }
};
</script>


