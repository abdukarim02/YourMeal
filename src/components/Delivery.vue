<template>
    <section class="deliver">
        <div class="deliver__content">
            <div class="deliver__content-bg">
                <img src="/public/deliver-bg.png" alt="">
            </div>
            <div class="deliver__content-info">
                <div class="deliver__info-top">
                    <h2 class="deliver__top-title">Доставка</h2>
                    <button class="deliver__info-btn">
                        <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                            <rect x="5.0752" y="5.28247" width="1" height="20" transform="rotate(-45 5.0752 5.28247)" fill="#B1B1B1" />
                            <rect x="5.78223" y="19.4246" width="1" height="20" transform="rotate(-135 5.78223 19.4246)" fill="#B1B1B1" />
                        </svg>
                    </button>
                </div>
                <form class="deliver__top-form" action="">
                    <div class="deliver__form-header">
                        <input class="deliver__header-input" type="text" placeholder="Ваше имя">
                        <input class="deliver__header-input" type="tel" placeholder="Телефон">
                    </div>
                    <div class="deliver__form-main">
                        <div class="deliver__main-body">
                            <input type="radio" name="drone" >
                            <label for="scales">Самовывоз</label>
                        </div>
                        <div class="deliver__main-body">
                            <input type="radio" name="drone" >
                            <label for="scales">Доставка</label>
                        </div>
                    </div>
                    <div class="deliver__form-footer">
                        <input class="deliver__header-input" type="text" placeholder="Улица, дом, квартира">
                        <div class="deliver__footer-body">
                            <input class="deliver__header-input" type="text" placeholder="Этаж">
                            <input class="deliver__header-input" type="text" placeholder="Домофон">
                        </div>
                    </div>
                </form>
                <button class="deliver__top-btn">Оформить</button>
            </div>
        </div>
    </section>
</template>