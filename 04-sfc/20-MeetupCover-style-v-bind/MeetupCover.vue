<script setup>
import {computed} from 'vue'

const props = defineProps({
  title: {
    type: String,
  },

  image: {
    type: String,
  },
})

const bgImage = computed(() =>
    props.image
        ? `linear-gradient(0deg, rgba(0, 0, 0, 0.4), rgba(0, 0, 0, 0.4)), url('${props.image}')`
        : `linear-gradient(0deg, rgba(0, 0, 0, 0.4), rgba(0, 0, 0, 0.4)), var(--default-cover)`
);
</script>

<template>
  <div class="meetup-cover">
    <h1 class="meetup-cover__title">{{ title }}</h1>
  </div>
</template>

<style scoped>
.meetup-cover {
  background-size: cover;
  background-position: center;
  /* Если изображение присутствует - берём его из CSS переменной, установленной на элемент в шаблоне */
  /* Иначе выводим изображение по умолчанию - var(--default-cover) */
  background-image: v-bind(bgImage);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 410px;
  max-width: 1216px;
  margin: 0 auto;
}

.meetup-cover__title {
  color: var(--white);
  font-weight: bold;
  font-size: 36px;
  line-height: var(--line-height);
  padding: 0 16px;
  text-align: center;
}

@media all and (min-width: 992px) {
  .meetup-cover__title {
    font-size: 72px;
    line-height: 84px;
  }
}
</style>
