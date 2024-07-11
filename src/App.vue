<script>
import './style.css';
import { ref, computed, onMounted } from 'vue';
import { Swiper, SwiperSlide } from "swiper/vue";
import "swiper/css";
import "swiper/css/scrollbar";
import "./style.css";
import { Scrollbar, Navigation } from "swiper/modules";

export default {
  components: {
    Swiper,
    SwiperSlide,
  },
  setup() {
    const timelines = ref([
      { id: 1, img: 'ng-logo.png', imgAlt: 'NG logo', title: 'Lift off', text: 'Таким образом реализация намеченных плановых заданий в значительной степени обуславливает создание.', data: '2019/01' },
      { id: 2, img: '', imgAlt: 'NG logo', title: 'Lofi Uppdate', text: 'Таким образом реализация намеченных плановых заданий в значительной степени обуславливает создание.', data: '2019/05' },
      { id: 3, img: '', imgAlt: 'NG logo', title: '+5', text: 'Таким образом реализация намеченных плановых заданий в значительной степени обуславливает создание.', data: '2020/02' },
      { id: 4, img: 'ng-logo.png', imgAlt: 'NG logo', title: 'Lift off', text: 'Таким образом реализация намеченных плановых заданий в значительной степени обуславливает создание.', data: '2020/06' },
      { id: 5, img: '', imgAlt: 'NG logo', title: 'Lift off', text: 'Таким образом реализация намеченных плановых заданий в значительной степени обуславливает создание.', data: '2024/01' },
      { id: 6, img: '', imgAlt: 'NG logo', title: 'Lift off', text: 'Таким образом реализация намеченных плановых заданий в значительной степени обуславливает создание.', data: '2023/01' },
      { id: 7, img: '', imgAlt: 'NG logo', title: 'Lift off', text: 'Таким образом реализация намеченных плановых заданий в значительной степени обуславливает создание.', data: '2024/01' },
      { id: 8, img: '', imgAlt: 'NG logo', title: 'Lift off', text: 'Таким образом реализация намеченных плановых заданий в значительной степени обуславливает создание.', data: '2025/01' },
    ]);


    const userPoints = ref([
      { city: 'Москва', employees: '6', x: 580, y: 140 },
      { city: 'Москва', employees: '5', x: 500, y: 140 },
      { city: 'Москва', employees: '3', x: 560, y: 140 },
      { city: 'Москва', employees: '3', x: 580, y: 210 },
      { city: 'Москва', employees: '3', x: 590, y: 140 },
      { city: 'Москва', employees: '3', x: 600, y: 150 },
      { city: 'Москва', employees: '3', x: 530, y: 100 },
      { city: 'Москва', employees: '3', x: 560, y: 120 },
      { city: 'Москва', employees: '8', x: 540, y: 150 },
      { city: 'Москва', employees: '3', x: 580, y: 200 },
      { city: 'Москва', employees: '3', x: 610, y: 180 },
      { city: 'Москва', employees: '3', x: 570, y: 160 },
      { city: 'Москва', employees: '3', x: 600, y: 170 },
      // Добавьте другие точки здесь
    ]);

    const firstYear = ref(null);
    const lastYear = ref(null);
    const firstDataOfYear = ref(null);
    const mapUsers = ref(false)
    const activePoint = ref(null);


    // Фильтрация cards чтобы показывалось от старых к новым
    const filteredTimelines = computed(() => {
      return timelines.value.sort((a, b) => new Date(a.data) - new Date(b.data));
    });

    const extractYears = () => {
      // нахождение самого старого и форматирование
      firstYear.value = filteredTimelines.value[0].data.split('/')[0];
      // нахождение самого нового и форматирование
      lastYear.value = filteredTimelines.value[filteredTimelines.value.length - 1].data.split('/')[0];



      const monthsByYear = {};

      // Группировка по годам и нахождение первого месяца для каждого года
      filteredTimelines.value.forEach((timeline) => {
        const [year, month] = timeline.data.split('/');
        const formattedDate = `${year}/${month.padStart(2, '0')}`;

        if (!monthsByYear[year]) {
          monthsByYear[year] = formattedDate;
        } else if (month < monthsByYear[year].split('/')[1]) {
          monthsByYear[year] = formattedDate;
        }
      });

      firstDataOfYear.value = monthsByYear;
      console.log(monthsByYear);
    };


    const tooltip = ref({
      visible: false,
      city: '',
      employees: '',
      x: 0,
      y: 0
    });

    const showTooltip = (event, point) => {
      tooltip.value.city = point.city;
      tooltip.value.employees = point.employees;
      tooltip.value.x = point.x + 107;
      tooltip.value.y = point.y + 105;
      tooltip.value.visible = true;
      activePoint.value = point; // Устанавливаем активный круг
      console.log(event, point)
    };

    const hideTooltip = () => {
      tooltip.value.visible = false;
      activePoint.value = null; // Сбрасываем активный круг
    };
    // Автоматический запуск функции при монтировании компонента
    onMounted(() => {
      extractYears();
    });

    return {
      timelines,
      firstYear,
      lastYear,
      filteredTimelines,
      mapUsers,
      userPoints,
      tooltip,
      showTooltip,
      hideTooltip,
      activePoint,
      modules: [Scrollbar, Navigation],
    };
  },
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
          <div class="third-block__mini-divs">
            <div class="third-block__card__mini-div">Start time · {{ this.firstYear }}</div>
            <div class="third-block__card__mini-div third-block__card__mini-div2">{{this.firstYear}} — {{ this.lastYear }}</div>
          </div>
          <div class="third-block__cards-parent df">
            <Swiper
                :scrollbar="{
                  el: '.swiper-scrollbar',
                  draggable: true,
                  hide: false,
                }"
                :navigation="{
                  nextEl: '.swiper-button-next',
                  prevEl: '.swiper-button-prev',
                }"
                :modules="modules"
                class="mySwiper">
              <Swiper-slide class="third-block__card" v-for="card in filteredTimelines" :key="card.id">
                <img v-if="card.img" :src="'src/assets/img/' + card.img" :alt="card.imgAlt">
                <h3 :class="{ mt34: !card.img}">{{ card.title }}</h3>
                <p>{{ card.text }}</p>
                <span>{{ card.data }}</span>
              </Swiper-slide>
              <div class="swiper-scrollbar"></div>
              <div class="swiper-button-next"></div>
              <div class="swiper-button-prev"></div>
            </Swiper>
          </div>
        </div>
      </section>
      <section class="fourth-block container__80">
        <div class="blocks__title">
          <h3>Цифры и преимущества_</h3>
        </div>
        <div class="fourth-block__map-numbers">
          <div class="fourth-block__map-numbers__mini-div">Network Maps</div>
          <div class="fourth-block__maps">
            <div class="fourth-block__map__nav df_jcsb">
              <div class="fourth-block__buttons df">
                <button @click="mapUsers = true" :class="{ 'fourth-block__map__button-active': this.mapUsers}">Пользователи</button>
                <button @click="mapUsers = false" :class="{ 'fourth-block__map__button-active': !this.mapUsers}">Сотрудники</button>
              </div>
              <div class="fourth-block__map__nav__text">
                <div class="fourth-block__map-numbers__mini-div fourth-block__map__nav__mini-div">#everywhere</div>
                <h3>Работаем в России и за рубежом!</h3>
              </div>
            </div>
            <div class="fourth-block__map">
              <div v-if="!mapUsers">
                <svg viewBox="0 0 1000 500" xmlns="http://www.w3.org/2000/svg">
                  <image href="./assets/img/map.svg" x="0" y="0" width="1000" height="500"/>
                  <g v-for="(point, index) in userPoints" :key="index">
                    <!-- Большой круг для захвата событий -->
                    <circle
                        :cx="point.x"
                        :cy="point.y"
                        :r="10"
                    fill="transparent"
                    @mouseenter="showTooltip($event, point)"
                    @mouseleave="hideTooltip"
                    />
                    <!-- Маленький круг для отображения -->
                    <circle
                        :cx="point.x"
                        :cy="point.y"
                        :r="point.employees"
                        :fill="activePoint === point ? '#6054FF' : 'white'"
                        class="city"
                        @mouseenter="showTooltip($event, point)"
                        @mouseleave="hideTooltip"
                    />
                  </g>
                </svg>
                <div class="tooltip fourth-block__map__text" v-if="tooltip.visible" :style="{ left: tooltip.x + 'px', top: tooltip.y + 'px'}">
                  <div class="fourth-block__map__mini-div fourth-block__map__tooltip__mini-div">x0521 · y2715</div>
                  <div class="df_jcc_ai">
                    {{ tooltip.city }} · {{ tooltip.employees }} <img src="./assets/img/user.svg" alt="User icon">
                  </div>
                </div>
              </div>
              <div v-else>
                <img src="./assets/img/map.png" alt="Picture of map">
                <div class="fourth-block__map__text">
                  <div class="fourth-block__map__mini-div">x0521 · y2715</div>
                  <p>Москва · 211 701</p>
                </div>
              </div>
            </div>
            <div class="fourth-block__numbers">
              <div class="df">
                <div class="fourth-block__numbers__card">
                  <div class="fourth-block__numbers__card__mini-div">folder/team</div>
                  <h3>40</h3>
                  <p>Сотрудников в команде</p>
                </div>
                <div class="fourth-block__numbers__card">
                  <div class="fourth-block__numbers__card__mini-div">stats/downloads</div>
                  <h3>2 000 000</h3>
                  <p>Скачиваний у приложений</p>
                </div>
                <div class="fourth-block__numbers__card">
                  <div class="fourth-block__numbers__card__mini-div">time/1:06</div>
                  <h3>4 лет</h3>
                  <p>Работаем больше возможного</p>
                </div>
              </div>
            </div>
          </div>
          <div class="fourth-block__advantages">
            <div class="fourth-block__advantages__mini-div">download/advantage</div>
            <div class="fourth-block__advantages-grid">
              <div class="fourth-block__advantages__card">
                <img src="./assets/img/home-icon.svg" alt="Icon">
                <h3>Удалёнка или офис</h3>
                <p>Работай из дома, кафе, офиса, откуда угодно</p>
              </div>
              <div class="fourth-block__advantages__card">
                <img src="./assets/img/circle-icon.svg" alt="Icon">
                <h3>Буквально откуда угодно</h3>
                <p>Работаем с сотрудниками не только из России, но и со всего мира, оплата придёт в любую точку Земли</p>
              </div>
              <div class="fourth-block__advantages__card">
                <img src="./assets/img/user-icon.svg" alt="Icon">
                <h3>Кстати об оплате</h3>
                <p>Еженедельно и никаких задержек</p>
              </div>
              <div class="fourth-block__advantages__card">
                <img src="./assets/img/home2-icon.svg" alt="Icon">
                <h3>Офис в центре Санкт-Петербурге</h3>
                <p>Недалеко от метро</p>
              </div>
              <div class="fourth-block__advantages__card">
                <img src="./assets/img/building-material-icon.svg" alt="Icon">
                <h3>Смотрим на твои реальные навыки</h3>
                <p>А не на высшее образование</p>
              </div>
              <div class="fourth-block__advantages__card">
                <img src="./assets/img/ladder-icon.svg" alt="Icon">
                <h3>Постоянно развиваемся</h3>
                <p>Ты сможешь расти вместе с нами как в карьере, так и в профессии</p>
              </div>
              <div class="fourth-block__advantages__card">
                <img src="./assets/img/robot-icon.svg" alt="Icon">
                <h3>Работаем с иностранным софтом и ИИ.</h3>
                <p>Еженедельно и никаких задержек</p>
              </div>
              <div class="fourth-block__advantages__card">
                <img src="./assets/img/cube-icon.svg" alt="Icon">
                <h3>Не аутсорс компания</h3>
                <p>Ты сможешь расти вместе с нами как в карьере, так и в профессии</p>
              </div>
            </div>
          </div>
        </div>
      </section>
      <section></section>
    </div>
  </main>
</template>


<style scoped>

</style>
