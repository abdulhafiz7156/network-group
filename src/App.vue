<script>
import { Swiper, SwiperSlide } from 'swiper/vue';
import 'swiper/css';
import 'swiper/css/scrollbar';
import 'swiper/css/pagination';
import 'swiper/css/navigation';
import './style.css';
import { Scrollbar, Pagination, Navigation } from 'swiper/modules';

export default {
  components: {
    Swiper,
    SwiperSlide,
  },
  setup() {
    return {
      timelines: [
        {
          id: 1,
          img: 'ng-logo.png', // name of image
          imgAlt: "NG logo", // you need to write there what is img
          title: 'Lift off',
          text: 'Таким образом реализация намеченных плановых заданий в значительной степени обуславливает создание.',
          data: '2019/01'
        },
        {
          id: 2,
          img: '',
          imgAlt: "NG logo",
          title: 'Lofi Uppdate',
          text: 'Таким образом реализация намеченных плановых заданий в значительной степени обуславливает создание.',
          data: '2019/05'
        },
        {
          id: 3,
          img: '',
          imgAlt: "NG logo",
          title: '+5',
          text: 'Таким образом реализация намеченных плановых заданий в значительной степени обуславливает создание.',
          data: '2020/02'
        },
        {
          id: 4,
          img: 'ng-logo.png',
          imgAlt: "NG logo",
          title: 'Lift off',
          text: 'Таким образом реализация намеченных плановых заданий в значительной степени обуславливает создание.',
          data: '2020/06'
        },
        {
          id: 5,
          img: '',
          imgAlt: "NG logo",
          title: 'Lift off',
          text: 'Таким образом реализация намеченных плановых заданий в значительной степени обуславливает создание.',
          data: '2024/01'
        },
        {
          id: 6,
          img: '',
          imgAlt: "NG logo",
          title: 'Lift off',
          text: 'Таким образом реализация намеченных плановых заданий в значительной степени обуславливает создание.',
          data: '2023/01'
        },
        {
          id: 7,
          img: '',
          imgAlt: "NG logo",
          title: 'Lift off',
          text: 'Таким образом реализация намеченных плановых заданий в значительной степени обуславливает создание.',
          data: '2024/01'
        },
        {
          id: 8,
          img: '',
          imgAlt: "NG logo",
          title: 'Lift off',
          text: 'Таким образом реализация намеченных плановых заданий в значительной степени обуславливает создание.',
          data: '2025/01'
        },
      ],
      modules: [Scrollbar, Pagination, Navigation],
      swiperOptions: {
        slidesPerView: 2,
        spaceBetween: 30,
        scrollbar: {
          el: '.swiper-scrollbar',
          draggable: true,
          hide: false,  // Показать полосу прокрутки всегда
        },

        loop: false,  // Отключаем бесконечную прокрутку
      },
    };
  },
  computed: {
    filteredTimelines() {
      return this.timelines.sort((a, b) => new Date(a.data) - new Date(b.data));
    }
  }
};
</script>
<template>
  <main>
    <div class="container">
      <section class="first-block">
        <div class="first-block-div df">
          <div class="first-block__text-div ">
            <div class="first-block__text-div__logo df_ai ">
              <img src="./assets/img/logo.png" alt="">
              <p>Network Group</p>
            </div>
            <div class="first-block__text-div__texts">
              <h1>Превратите возможности в планы</h1>
              <p>Таким образом реализация намеченных плановых заданий в значительной степени обуславливает создание систем массового участия.</p>
              <button>Открытые вакансии [12]</button>
            </div>
          </div>
          <div class="first-block__img-div">
            <img src="./assets/img/bg.png" alt="Background image">
          </div>
        </div>
      </section>
      <section class="second-block container__80">
        <div class="blocks__title">
          <h3>Наши продукты_</h3>
        </div>
        <div class="second-block__cards df">
          <div class="second-block__card green-card">
            <div class="card__mini-div card__mini-div--green">Product • 001</div>
            <div class="second-block__card__texts-img df">
              <div class="second-block__card__texts">
                <img src="./assets/img/ng-logo.png" alt="NG logo">
                <h2>Network Graphics</h2>
                <p>Таким образом реализация намеченных плановых заданий в значительной степени обуславливает создание.</p>
              </div>
              <div class="second-block__card__img df">
                <img src="./assets/img/ng-vector.png" alt="NG Vector">
              </div>
            </div>
          </div>
          <div class="second-block__card white-card">
            <div class="card__mini-div card__mini-div--white">Product • 002</div>
            <div class="second-block__card__texts-img df">
              <div class="second-block__card__texts">
                <img src="./assets/img/meta-logo.png" alt="NG logo">
                <h2>Meta Network</h2>
                <p>Таким образом реализация намеченных плановых заданий в значительной степени обуславливает создание.</p>
              </div>
              <div class="second-block__card__img df">
                <img src="./assets/img/meta-vector.png" alt="Meta Vector">
              </div>
            </div>
          </div>
          <div class="second-block__card yellow-card">
            <div class="card__mini-div card__mini-div--yellow">Product • 003</div>
            <div class="second-block__card__texts-img df">
              <div class="second-block__card__texts">
                <img src="./assets/img/startapp.png" alt="StartApp logo">
                <h2>StartApp</h2>
                <p>Таким образом реализация намеченных плановых заданий в значительной степени обуславливает создание.</p>
              </div>
              <div class="second-block__card__img df">
                <img src="./assets/img/startapp-vector.png" alt="StartApp Vector">
              </div>
            </div>
          </div>
          <div class="second-block__card violet-card">
            <div class="card__mini-div card__mini-div--violet">Product • 004</div>
            <div class="second-block__card__texts-img df">
              <div class="second-block__card__texts">
                <img src="./assets/img/startapp.png" alt="StartApp logo">
                <h2>Зарубежный проект</h2>
                <p>Таким образом реализация намеченных плановых заданий в значительной степени обуславливает создание.</p>
              </div>
              <div class="second-block__card__img df">
                <img src="./assets/img/foreign-vector.png" alt="Foreign Vector">
              </div>
            </div>
          </div>
        </div>
      </section>
      <section class="third-block container__80">
        <div class="blocks__title">
          <h3>Таймлайн_</h3>
        </div>
        <div class="third-block__cards">
          <Swiper :modules="modules" :options="swiperOptions">
            <SwiperSlide class="third-block__card" v-for="card in filteredTimelines" :key="card.id">
              <img v-if="card.img" :src="'src/assets/img/' + card.img" :alt="card.imgAlt">
              <h3 :class="{ mt34: !card.img}">{{ card.title }}</h3>
              <p>{{ card.text }}</p>
              <span>{{ card.data }}</span>
            </SwiperSlide>
            <!-- Pagination -->
            <div class="swiper-pagination"></div>
            <!-- Scrollbar -->
            <div class="swiper-scrollbar"></div>
          </Swiper>
        </div>
      </section>
      <section></section>
      <section></section>
    </div>
  </main>
</template>


<style scoped>

</style>
