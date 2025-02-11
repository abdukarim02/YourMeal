<template>
    <section class="deliver" v-if="isVisible">
        <div class="deliver__content">
            <div class="deliver__content-bg">
                <img src="/public/deliver-bg.png" alt="">
            </div>
            <div class="deliver__content-info">
                <div class="deliver__info-top">
                    <h2 class="deliver__top-title">Доставка</h2>
                    <button class="deliver__info-btn" @click="closePopup">
                        <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                            <rect x="5.0752" y="5.28247" width="1" height="20" transform="rotate(-45 5.0752 5.28247)" fill="#B1B1B1" />
                            <rect x="5.78223" y="19.4246" width="1" height="20" transform="rotate(-135 5.78223 19.4246)" fill="#B1B1B1" />
                        </svg>
                    </button>
                </div>
                <form class="deliver__top-form" @submit.prevent="submitForm">
                    <div class="deliver__form-header">
                        <input class="deliver__header-input" type="text" placeholder="Ваше имя" v-model="name" required>
                        <input 
                            class="deliver__header-input" 
                            type="tel" 
                            placeholder="Телефон" 
                            v-model="phone" 
                            @input="validatePhone" 
                            @blur="checkPhoneFormat"
                            required
                        >
                        <p v-if="phoneError" class="error-message">{{ phoneError }}</p>
                    </div>
                    <div class="deliver__form-main">
                        <div class="deliver__main-body">
                            <input type="radio" name="delivery" value="pickup" v-model="deliveryType">
                            <label>Самовывоз</label>
                        </div>
                        <div class="deliver__main-body">
                            <input type="radio" name="delivery" value="delivery" v-model="deliveryType">
                            <label>Доставка</label>
                        </div>
                    </div>
                    <div class="deliver__form-footer" v-if="deliveryType === 'delivery'">
                        <input class="deliver__header-input" type="text" placeholder="Улица, дом, квартира" v-model="address" required>
                        <div class="deliver__footer-body">
                            <input class="deliver__header-input" type="text" placeholder="Этаж" v-model="floor" required>
                            <input class="deliver__header-input" type="text" placeholder="Домофон" v-model="intercom" required>
                        </div>
                    </div>
                    <button class="deliver__top-btn" type="submit">Оформить</button>
                </form>
            </div>
        </div>
    </section>
</template>
<script>
export default {
    data() {
        return {
            isVisible: true,
            name: '',
            phone: '',
            phoneError: '',
            deliveryType: '',
            address: '',
            floor: '',
            intercom: ''
        };
    },
    methods: {
        closePopup() {
            this.isVisible = false;
        },
        validatePhone() {
            // Оставляем только + и цифры
            this.phone = this.phone.replace(/[^0-9+]/g, '');
            
            // Если первый символ не "+", добавляем его
            if (this.phone.length > 0 && this.phone[0] !== '+') {
                this.phone = '+' + this.phone.replace(/\+/g, ''); // Убираем все лишние плюсы
            }

            // Ограничиваем длину 12 символами
            if (this.phone.length > 12) {
                this.phone = this.phone.slice(0, 12);
            }
        },
        checkPhoneFormat() {
            const phoneRegex = /^\+[0-9]{11}$/; // + и 11 цифр (всего 12 символов)
            if (!phoneRegex.test(this.phone)) {
                this.phoneError = 'Введите корректный номер телефона (пример: +998901234567)';
            } else {
                this.phoneError = '';
            }
        },
        submitForm() {
            if (this.phoneError) {
                alert('Исправьте ошибки в номере телефона');
                return;
            }
            if (this.deliveryType === 'delivery' && (!this.address || !this.floor || !this.intercom)) {
                alert('Заполните все поля для доставки');
                return;
            }
            alert('Заказ оформлен!');
            this.closePopup();
            setTimeout(() => {
                location.reload();
            }, 500); // Добавляем небольшую задержку перед перезагрузкой
            }
        }
};
</script>

