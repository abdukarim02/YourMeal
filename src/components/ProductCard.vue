<template>
    <div class="product-card" v-if="product">
        <div class="product-card__content">
            <div class="product-card__conten-body">
                <button class="product-card__content-close" @click="$emit('close')">
                    <svg width="29" height="30" viewBox="0 0 29 30" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <rect x="7.07422" y="8.28249" width="1" height="20" transform="rotate(-45 7.07422 8.28249)" fill="#B1B1B1" />
                        <rect x="7.78125" y="22.4246" width="1" height="20" transform="rotate(-135 7.78125 22.4246)" fill="#B1B1B1" />
                    </svg>
                </button>
                <div class="product-card__content-bg">
                    <h2 class="product-card__bg-name">{{ product.name }}</h2>
                    <img :src="product.img" :alt="product.name" class="product-card__bg-img">
                </div>
                <div class="product-card__content-info">
                    <p class="product-card__info-text">{{ product.textInfo }} </p>
                    <ul class="product-card__info-compound">
                        <h5 class="product-card__compound-name">Состав:</h5>
                        <li v-for="(ingredient, index) in product.ingredients" :key="index" class="product-card__compound-list">{{ ingredient }}</li>
                    </ul>
                    <div class="product-card__info-gram">{{ product.weight }}г, ккал 430</div>
                </div>
            </div> 
            <div class="product-card__content-button">
                <div class="product-card__button">
                    <button class="product-card__button-btn" @click="$emit('add-to-cart', product)">Добавить</button>
                    <div class="product-card__button-corusel">
                        <button @click="decreaseQuantity">-</button>
                        <span>{{ quantity }}</span>
                        <button @click="increaseQuantity">+</button>
                    </div>
                </div>
                <p class="product-card__button-price">{{ product.price }}₽</p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        product: Object
    },
    data() {
        return {
            quantity: 1
        };
    },
    methods: {
        increaseQuantity() {
            this.quantity++;
        },
        decreaseQuantity() {
            if (this.quantity > 1) {
                this.quantity--;
            }
        }
    }
};
</script>