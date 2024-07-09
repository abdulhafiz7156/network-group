<script>
import './style.css';
import { ref, computed, onMounted } from 'vue';

export default {
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

    const firstYear = ref(null);
    const lastYear = ref(null);
    const firstDataOfYear = ref(null);
    const mapUsers = ref(true)

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

    // Автоматический запуск функции при монтировании компонента
    onMounted(() => {
      extractYears();
    });

    return {
      timelines,
      firstYear,
      lastYear,
      filteredTimelines,
      mapUsers
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
            <div class="third-block__card" v-for="card in filteredTimelines" :key="card.id">
<!--              <div class="third-block__card__mini-div third-block">{{ this.firstYear }}</div>-->
              <img v-if="card.img" :src="'src/assets/img/' + card.img" :alt="card.imgAlt">
              <h3 :class="{ mt34: !card.img}">{{ card.title }}</h3>
              <p>{{ card.text }}</p>
              <span>{{ card.data }}</span>
            </div>
          </div>
        </div>
      </section>
      <section class="fourth-block container__80">
        <div class="blocks__title">
          <h3>Цифры и преимущества_</h3>
        </div>
        <div class="fourth-block__map-numbers">
          <div class="fourth-block__maps">
            <div class="fourth-block__map__nav df_jcsb">
              <div class="fourth-block__buttons df">
                <button @click="mapUsers = true" :class="{ 'fourth-block__map__button-active': this.mapUsers}">Пользователи</button>
                <button @click="mapUsers = false" :class="{ 'fourth-block__map__button-active': !this.mapUsers}">Сотрудники</button>
              </div>
              <div class="fourth-block__map__nav__text">
                <h3>Работаем в России и за рубежом!</h3>
              </div>
            </div>
            <div class="fourth-block__map">
              <div v-if="mapUsers">
                <img src="./assets/img/map.png" alt="">
                <div class="fourth-block__map__text">
                  <div>x0521 · y2715</div>
                  <p>Москва · 211 701</p>
                </div>
              </div>
              <div v-if="!mapUsers">
                <img src="./assets/img/map.png" alt="">
              </div>
            </div>
          </div>
          <div class="fourth-block__numbers"></div>
        </div>
      </section>
      <section></section>
    </div>
  </main>
</template>


<style scoped>

</style>
