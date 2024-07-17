<template>
  <div ref="blockRef" class="block">
    <slot />
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';
import gsap from 'gsap';

export default {
  setup() {
    const blockRef = ref(null);

    const animateBlock = () => {
      const tl = gsap.timeline({ paused: true });
      tl.from(blockRef.value, {
        duration: 1.5,
        y: 150,
        opacity: 0,
        ease: "power3.out",
        scrollTrigger: {
          start: 'top 80%',
          end: 'bottom 20%',
          toggleActions: 'play none none reset',
        },
      });

      const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            tl.play();
          }
        });
      });

      observer.observe(blockRef.value);
    };

    onMounted(animateBlock);

    return {
      blockRef,
    };
  },
};
</script>

<style scoped>

</style>