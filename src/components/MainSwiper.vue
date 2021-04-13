<template>
  <swiper>
    <swiper-item v-for="(item, index) in swiperList" :key="index">
      <img :src="item.img" alt="">
    </swiper-item>
  </swiper>
</template>

<script>
import Swiper from './Swiper.vue';
import SwiperItem from './SwiperItem.vue';
export default {
  name: "MainSwiper",
  components: {Swiper, SwiperItem},
  created() {},
  data() {
    return {
      swiperList: [
        {img: require('../assets/img/pic1.jpg')},
        {img: require('../assets/img/pic2.jpg')},
        {img: require('../assets/img/pic3.jpg')},
      ]
    };
  },
  props: {},
  methods: {},
};
</script>

<style lang="scss" scoped></style>