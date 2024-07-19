<script>
import './style.css';
import { ref, computed, onMounted, reactive, watch } from 'vue';
import { Swiper, SwiperSlide } from "swiper/vue";
import "swiper/css";
import "swiper/css/scrollbar";
import "./style.css";
import { Scrollbar, Navigation } from "swiper/modules";
import { gsap } from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
import { TextPlugin } from 'gsap/TextPlugin';
import AnimatedBlock from './components/AnimatedBlock.vue'


gsap.registerPlugin(ScrollTrigger,TextPlugin);

export default {
  components: {
    Swiper,
    SwiperSlide,
    AnimatedBlock
  },
  setup() {
    const timelines = ref([
      { id: 1, img: 'ng-logo.png', imgAlt: 'NG logo', title: 'Lift off', text: 'Таким образом реализация намеченных плановых заданий в значительной степени обуславливает создание.', data: '2019/01' },
      { id: 4, img: '', imgAlt: 'NG logo', title: 'Lift off', text: 'Таким образом реализация намеченных плановых заданий в значительной степени обуславливает создание.', data: '2020/06' },
      { id: 4, img: 'ng-logo.png', imgAlt: 'NG logo', title: 'Lift off', text: 'Таким образом реализация намеченных плановых заданий в значительной степени обуславливает создание.', data: '2020/06' },
      { id: 4, img: 'ng-logo.png', imgAlt: 'NG logo', title: 'Lift off', text: 'Таким образом реализация намеченных плановых заданий в значительной степени обуславливает создание.', data: '2020/06' },
      { id: 4, img: 'ng-logo.png', imgAlt: 'NG logo', title: 'Lift off', text: 'Таким образом реализация намеченных плановых заданий в значительной степени обуславливает создание.', data: '2020/06' },
      { id: 4, img: 'ng-logo.png', imgAlt: 'NG logo', title: 'Lift off', text: 'Таким образом реализация намеченных плановых заданий в значительной степени обуславливает создание.', data: '2020/06' },
      { id: 4, img: 'ng-logo.png', imgAlt: 'NG logo', title: 'Lift off', text: 'Таким образом реализация намеченных плановых заданий в значительной степени обуславливает создание.', data: '2020/06' },
    ]);

    const userPoints = ref([
      { city: 'Москва', employees: '6', x: 780, y: 240 },
      { city: 'Москва', employees: '5', x: 700, y: 240 },
      { city: 'Москва', employees: '3', x: 760, y: 240 },
      { city: 'Москва', employees: '3', x: 780, y: 210 },
      { city: 'Москва', employees: '3', x: 790, y: 240 },
      { city: 'Москва', employees: '3', x: 700, y: 250 },
      { city: 'Москва', employees: '3', x: 730, y: 200 },
      { city: 'Москва', employees: '3', x: 760, y: 220 },
      { city: 'Москва', employees: '8', x: 740, y: 250 },
      { city: 'Москва', employees: '3', x: 780, y: 200 },
      { city: 'Москва', employees: '3', x: 710, y: 280 },
      { city: 'Москва', employees: '3', x: 770, y: 260 },
      { city: 'Москва', employees: '3', x: 700, y: 270 },
      // Добавьте другие точки здесь
    ]);

    const vacancies = ref([
      {
        id: 1,
        title: "Разработчик шейдеров",
        description: "Разработка и оптимизация шейдеров для графических движков.",
        details: {
          location: "Москва",
          type: "Фултайм",
          experience: "Опыт от 3 лет"
        },
        requirementsTitle: "Вы нам подходите, если",
        requirementsDescription: "Ищем опытного разработчика шейдеров.",
        requirements: [
          "У вас глубокие знания языка программирования HLSL/GLSL или других языков написания шейдеров;",
          "Есть опыт работы с ReShade и/или ENB;",
          "Имеете навыки работы с графическими движками и понимаете процессы рендеринга;",
          "Имеете портфолио с примерами работ по созданию или оптимизации шейдеров."
        ],
        buttonText: "Написать сейчас"
      },
      {
        id: 2,
        title: "Контент Менеджер",
        description: "Таким образом реализация намеченных плановых заданий.",
        details: {
          location: "Москва",
          type: "Фултайм",
          experience: "Опыт от 1 года"
        },
        requirementsTitle: "Вы нам подходите, если",
        requirementsDescription: "Таким образом реализация намеченных плановых заданий.",
        requirements: [
          "У вас глубокие знания языка программирования HLSL/GLSL или других языков написания шейдеров;",
          "Есть опыт работы с ReShade и/или ENB;",
          "Имеете навыки работы с графическими движками и понимаете процессы рендеринга;",
          "Имеете портфолио с примерами работ по созданию или оптимизации шейдеров."
        ],
        buttonText: "Написать сейчас"
      },
      {
        id: 3,
        title: "Проект Менеджер",
        description: "Организация и контроль выполнения проектов.",
        details: {
          location: "Санкт-Петербург",
          type: "Фултайм",
          experience: "Опыт от 2 лет"
        },
        requirementsTitle: "Вы нам подходите, если",
        requirementsDescription: "Ищем опытного проект-менеджера.",
        requirements: [
          "У вас есть опыт работы с Agile/Scrum;",
          "Вы умеете планировать и распределять ресурсы;",
          "Обладаете отличными коммуникативными навыками;",
          "Имеете портфолио успешно завершенных проектов."
        ],
        buttonText: "Отправить резюме"
      },
      {
        id: 4,
        title: "UX/UI Дизайнер",
        description: "Разработка пользовательских интерфейсов и улучшение UX.",
        details: {
          location: "Удаленно",
          type: "Частичная занятость",
          experience: "Опыт от 4 лет"
        },
        requirementsTitle: "Вы нам подходите, если",
        requirementsDescription: "Ищем талантливого дизайнера.",
        requirements: [
          "Вы умеете работать с Figma и Sketch;",
          "Есть опыт работы в крупных проектах;",
          "Понимаете принципы UX и UI;",
          "Имеете портфолио с примерами работ."
        ],
        buttonText: "Написать сейчас"
      },
      {
        id: 5,
        title: "Маркетолог",
        description: "Разработка и реализация маркетинговых стратегий.",
        details: {
          location: "Москва",
          type: "Фултайм",
          experience: "Опыт от 3 лет"
        },
        requirementsTitle: "Вы нам подходите, если",
        requirementsDescription: "Ищем опытного маркетолога.",
        requirements: [
          "У вас есть опыт работы в digital marketing;",
          "Вы умеете анализировать данные и делать выводы;",
          "Понимаете принципы SEO и SMM;",
          "Имеете портфолио успешных кейсов."
        ],
        buttonText: "Отправить резюме"
      },
      {
        id: 6,
        title: "DevOps Инженер",
        description: "Автоматизация и управление инфраструктурой.",
        details: {
          location: "Санкт-Петербург",
          type: "Фултайм",
          experience: "Опыт от 5 лет"
        },
        requirementsTitle: "Вы нам подходите, если",
        requirementsDescription: "Ищем опытного DevOps инженера.",
        requirements: [
          "У вас есть опыт работы с Docker и Kubernetes;",
          "Понимаете принципы CI/CD;",
          "Знаете скриптовые языки (Bash, Python);",
          "Имеете портфолио успешно выполненных проектов."
        ],
        buttonText: "Написать сейчас"
      }
    ])

    const firstYear = ref(null);
    const lastYear = ref(null);
    const firstDataOfYear = ref(null);
    const mapUsers = ref(false)
    const activePoint = ref(null);
    const isSidebarOpen = ref(false);
    const selectedVacancy = reactive({});
    const sidebar = ref(null);
    const addTitleRef1 = ref(null);
    const addTitleRef2 = ref(null);
    const addTitleRef3 = ref(null);
    const addTitleRef4 = ref(null);
    const currentYear = ref(new Date().getFullYear());
    const swiperRef = ref(null)
    const scrollbarThumb = ref(null);
    const cursorCeo = ref(null);
    const cursorUser = ref(null);
    const cursorDev = ref(null);
    const cursorUserMobile = ref(null)

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
    };

    const hideTooltip = () => {
      tooltip.value.visible = false;
      activePoint.value = null; // Сбрасываем активный круг
    };

    const openSidebar = (card) => {
      // Close any currently open sidebar first
      if (isSidebarOpen.value) {
        closeSidebar();
      }

      // Open the new sidebar
      Object.assign(selectedVacancy, card);
      isSidebarOpen.value = true;

      // Add the click handler for outside clicks
      setTimeout(() => {
          document.addEventListener('click', handleClickOutside);
      }, 0);
    };

    const closeSidebar = () => {
      isSidebarOpen.value = false;
      Object.keys(selectedVacancy).forEach(key => {
        delete selectedVacancy[key];
      });

      // Remove the click handler for outside clicks
      document.removeEventListener('click', handleClickOutside);
    };

    const handleClickOutside = (event) => {
      // console.log(sidebar.value)
      console.log(event)
      if (sidebar.value && !event.target.closest('.vacancy-block-grid')) {
        console.log("Click detected outside sidebar and not on a vacancy card");
        closeSidebar();
      } else {
        // closeSidebar();
      }
    };


    const animateTitle = (element, newText) => {
      const h3 = element.querySelector('h3');
      const cursor = '<span class="cursor">_</span>';
      gsap.to(h3, {
        duration: 3,
        text: newText + cursor,
        ease: 'power3.out',
        scrollTrigger: {
          trigger: element,
          start: 'top 100%',
          toggleActions: 'play none none reset',
        },
        onComplete: () => {
          gsap.to(h3.querySelector('.cursor'), {
            opacity: 0,
            repeat: -1,
            yoyo: true,
            ease: 'power1.inOut',
            duration: 0.5,
          });
        },
      });
    };

    const getPic = (index) => {
      console.log(index)
      return 'https://network-group.vercel.app/' + 'assets/img/' + index;
              // https://network-group.vercel.app/     assets/img/ ng-logo.png
    }

    const animateCount = (element, endValue) => {
      gsap.fromTo(
          element,
          { innerText: 0 },
          {
            innerText: endValue,
            duration: 2,
            ease: 'power3.out',
            scrollTrigger: {
              trigger: element,
              start: 'top 80%',
              end: 'bottom 20%',
              toggleActions: 'play none none none',
            },
            snap: { innerText: 1 }, // округление до целых чисел
            modifiers: {
              innerText: value => parseFloat(value).toFixed(0) // без форматирования
            },
            onUpdate: function () {
              element.textContent = Math.round(element.innerText).toLocaleString('ru-RU'); // обновление textContent с пробелами
            },
          }
      );
    };

    const scrollToTarget = () => {
      document.getElementById('vacancies').scrollIntoView({ behavior: 'smooth' });
    }

    const getCircleRadius = (employees) => {
      if (employees <= 3) {
        return 3;
      } else if (employees <= 6) {
        return 4.3;
      } else {
        return 5.5;
      }
    };

    const slideNext = () => {
      console.log("fak")
      swiperRef.value.swiper.slideNext();
    };

    const slidePrev = () => {
      console.log("prev")
      swiperRef.value.swiper.slidePrev();
    };




    onMounted(() => {
      extractYears();
      document.addEventListener('click', handleClickOutside);

      const titles = [
        { el: addTitleRef1.value, text: "Наши продукты" },
        { el: addTitleRef2.value, text: "Таймлайн" },
        { el: addTitleRef3.value, text: "Цифры и преимущества" },
        { el: addTitleRef4.value, text: "Открытые вакансии" },
      ];

      titles.forEach(({ el, text }) => {
        if (el) {
          animateTitle(el, text);
        } else {
          console.warn('Element reference is null:', el);
        }
      });

      document.querySelectorAll('.count').forEach(el => {
        animateCount(el, el.getAttribute('data-end'));
      });

      gsap.set(cursorCeo.value, { x: '-100%', y: '-100%' });
      gsap.set(cursorUser.value, { x: '100%', y: '-100%' });
      // gsap.set(cursorUserMobile.value, { x: '100%', y: '-100%' });
      gsap.set(cursorDev.value, { x: '-100%', y: '100%' });

      gsap.to(cursorCeo.value, { duration: 2, x: '-50%', y: '450%', ease: 'power2.inOut' });
      gsap.to(cursorUser.value, { duration: 2, x: '-30%', y: '-750%', ease: 'power2.inOut', delay: 0.5 });
      gsap.to(cursorUserMobile.value, { duration: 2, x: '0%', y: '-500%', ease: 'power2.inOut', delay: 0.5 });
      gsap.to(cursorDev.value, { duration: 2, x: '310%', y: '-240%', ease: 'power2.inOut', delay: 0.5 });
    });

    watch(isSidebarOpen, (newVal) => {
      if (newVal) {
        document.addEventListener('click', handleClickOutside);
      } else {
        document.removeEventListener('click', handleClickOutside);
      }
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
      vacancies,
      isSidebarOpen,
      selectedVacancy,
      openSidebar,
      closeSidebar,
      sidebar,
      modules: [Scrollbar, Navigation],
      addTitleRef1,
      addTitleRef2,
      addTitleRef3,
      addTitleRef4,
      animateTitle,
      currentYear,
      getPic,
      animateCount,
      scrollToTarget,
      getCircleRadius,
      slideNext,
      slidePrev,
      scrollbarThumb,
      cursorCeo,
      cursorUser,
      cursorDev,
      cursorUserMobile
    };
  },
};
</script>
<template>
  <main>
    <div class="container">
      <section class="first-block ">
        <div class="first-block__div df">
          <div class="first-block__text-div ">
            <div class="first-block__text-div__logo df_ai ">
              <img src="./assets/img/logo.png" alt="">
              <p>Network Group</p>
            </div>
            <div class="first-block__text-div__texts">
              <h1>Превратите возможности в планы</h1>
              <p>Таким образом реализация намеченных плановых заданий в значительной степени обуславливает создание систем массового участия.</p>
              <button @click="scrollToTarget">Открытые вакансии [12]</button>
              <div class="first-block__img-div-mobile">
                <img src="./assets/img/cursor-user.png" alt="Cursor" ref="cursorUserMobile">
              </div>
            </div>
          </div>
          <div class="first-block__img-div">
            <img src="./assets/img/bg.png" alt="Background image" class="first-block__img__div__img">
            <div class="cursors">
              <img src="./assets/img/cursor-ceo.svg" alt="Cursor of Ceo" class="cursor cursor-ceo" ref="cursorCeo" />
              <img src="./assets/img/cursor-user.svg" alt="Cursor of User" class="cursor cursor-user" ref="cursorUser" />
              <img src="./assets/img/cursor-dev.svg" alt="Cursor of Developer" class="cursor cursorDev" ref="cursorDev" />
            </div>
          </div>
        </div>
      </section>
      <section class="second-block">
        <div ref="addTitleRef1" class="blocks__title">
          <h3>_</h3>
        </div>
        <AnimatedBlock>
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
        </AnimatedBlock>
      </section>
      <section class="third-block">
        <div  ref="addTitleRef2" class="blocks__title">
          <h3>_</h3>
        </div>
        <AnimatedBlock>
          <div class="third-block__cards">
            <div class="third-block__mini-divs">
              <div class="third-block__card__mini-div">Start time · {{ this.firstYear }}</div>
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
                  ref="swiperRef"
                  :modules="modules"
                  :breakpoints="{
                    768: {
                      slidesPerView: 1,
                    },
                    1024: {
                      slidesPerView: 2,
                    },
                    1300: {
                      slidesPerView: 3,
                    },
                    1920: {
                      slidesPerView: 'auto',
                    }
                  }"
                  class="mySwiper"
              >
                <Swiper-slide class="third-block__card"
                              v-for="card in filteredTimelines"
                              :key="card.id">
                  <img v-if="card.img"
                       :src="getPic(card.img)"
                       :alt="card.imgAlt"
                  >
                  <h3 :class="{ mt34: !card.img}">{{ card.title }}</h3>
                  <p>{{ card.text }}</p>
                  <span>{{ card.data }}</span>
                </Swiper-slide>
              </Swiper>
                  <div class="swiper-scrollbar"></div>
                  <div class="swiper-button-next" @click="slideNext"><img src="./assets/img/right-side-icon.svg" alt=""></div>
                  <div class="swiper-button-prev" @click="slidePrev"><img src="./assets/img/left-side-icon.svg" alt=""></div>
            </div>
          </div>
        </AnimatedBlock>
      </section>
      <section class="fourth-block ">
        <div  ref="addTitleRef3" class="blocks__title">
          <h3>_</h3>
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
                <svg viewBox="0 0 1339 712" xmlns="http://www.w3.org/2000/svg">
                  <image href="./assets/img/map.svg" x="0" y="0" width="1339" height="712"/>
                  <g v-for="(point, index) in userPoints" :key="index">
                    <!-- Большой круг для захвата событий -->
                    <rect
                        :x="point.x - 10"
                        :y="point.y - 10"
                        width="20"
                        height="20"
                        class="city"
                        fill="transparent"
                        @mouseenter="showTooltip($event, point)"
                        @mouseleave="hideTooltip"
                    />
                    <!-- Маленький круг для отображения -->
                    <circle
                        :cx="point.x"
                        :cy="point.y"
                        :r="getCircleRadius(point.employees)"
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
                <svg viewBox="0 0 1339 712" xmlns="http://www.w3.org/2000/svg">
                  <image href="./assets/img/map1.svg" x="0" y="0" width="1339" height="712"/>
                </svg>
              </div>
            </div>
          </div>
          <AnimatedBlock>
            <div class="fourth-block__numbers">
              <div class="df">
                <div class="fourth-block__numbers__card">
                  <div class="fourth-block__numbers__card__mini-div">folder/team</div>
                  <h3 class="count" data-end="40">0</h3>
                  <p>Сотрудников в команде</p>
                </div>
                <div class="fourth-block__numbers__card">
                  <div class="fourth-block__numbers__card__mini-div">stats/downloads</div>
                  <h3 class="count" data-end="2000000">0</h3>
                  <p>Скачиваний у приложений</p>
                </div>
                <div class="fourth-block__numbers__card">
                  <div class="fourth-block__numbers__card__mini-div">time/1:06</div>
                  <h3 class="count" data-end="4">0</h3>
                  <p>Работаем больше возможного</p>
                </div>
              </div>
            </div>
          </AnimatedBlock>
          <AnimatedBlock>
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
          </AnimatedBlock>
        </div>
      </section>
      <section class="vacancy-block" id="vacancies">
        <div  ref="addTitleRef4" class="blocks__title">
          <h3>_</h3>
        </div>
        <AnimatedBlock>
        <div class="vacancy-block-grid">
            <div class="vacancy-block-grid__card" v-for="(card, index) in vacancies" :key="index" @click="openSidebar(card)" >
              <div class="vacancy-block-grid__card__mini-div">folder/vacancies</div>
              <h3>{{card.title}}</h3>
              <p>{{card.description}}</p>
              <div class="vacancy-block-grid__card__subtitles df">
                <div v-for="(details, id) in card.details" :key="id">
                  {{details}}
                </div>
              </div>
            </div>
        </div>
        </AnimatedBlock>
        <div :class="['sidebar', { 'sidebar--open': isSidebarOpen }]" ref="sidebar">
            <button class="sidebar__close-btn" @click="closeSidebar">
              <img src="./assets/img/right-icon.png" alt="Right side icon">
              <img src="./assets/img/right-icon.png" alt="Right side icon">
            </button>
            <div class="sidebar__texts">
              <div class="sidebar__texts__mini-div">folder/vacancies</div>
              <div class="sidebar__texts__section">
                <h3>{{selectedVacancy.title}}</h3>
                <p>{{selectedVacancy.description}}</p>
                <div>
                  <ul>
                    <li v-for="details in selectedVacancy.details" :key="selectedVacancy.id">
                      {{details}}
                    </li>
                  </ul>
                </div>
              </div>
              <div>
                <h3>{{selectedVacancy.requirementsTitle}}</h3>
                <p>{{selectedVacancy.requirementsDescription}}</p>
                <div>
                  <ul>
                    <li v-for="details in selectedVacancy.requirements" :key="selectedVacancy.id">
                      {{details}}
                    </li>
                  </ul>
                </div>
              </div>
              <button>Написать сейчас</button>
            </div>
        </div>
      </section>
      <footer>
          <div class="df_jcsb">
          <div class="footer__text df_jcsb">
            <p>© {{ currentYear }} «Network Group»</p>
            <p>ng@ng.ru</p>
          </div>
          <div class="footer__links df">
<!--            <a href="">-->
<!--              <img src="./assets/img/vk-icon.svg" alt="Icon">-->
<!--            </a>-->
            <a href="http://t.me/ntw_jobs" target="_blank">
              <img src="./assets/img/telegram-icon.svg" alt="Icon">
            </a>
<!--            <a href="">-->
<!--              <img src="./assets/img/discord-icon.svg" alt="Icon">-->
<!--            </a>-->
          </div>
        </div>
      </footer>
      <div v-if="isSidebarOpen" class="overlay" @click="closeSidebar"></div>
    </div>
  </main>
</template>


<style scoped>

</style>
