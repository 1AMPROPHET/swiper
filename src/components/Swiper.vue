<template>
  <div class="hy-swiper">
    <div class="swiper">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "Swiper",
  created() {},
  mounted() {
    setTimeout(() => {
      this.getImage()
      this.startTimer()
    }, 200)
  },
  data() {
    return {
      count: 0,
      timer: null,
      delay: 3000,
      imgaeWidth: 0,
      swiperStyle: {},
      isScroll: false,
      currentIndex: 1
    };
  },
  props: {
  },
  methods: {
    getImage() {
      let swiperEl = document.querySelector('.swiper')
      let slideEls = document.getElementsByClassName('slide')
      this.count = slideEls.length
      if (this.count > 1) {
        let cloneFirst = slideEls[0].cloneNode(true)
        let cloneLast = slideEls[this.count - 1].cloneNode(true)
        swiperEl.insertBefore(cloneLast, slideEls[0])
        swiperEl.appendChild(cloneFirst)
        this.swiperStyle = swiperEl.style
        this.imgaeWidth = swiperEl.offsetWidth
      }
      this.setTransform(-this.imgaeWidth)
    },
    setTransform(position) {
      this.swiperStyle.transform = 'translate3d(' + position + 'px, 0, 0)'
      // this.swiperStyle.transform = `translate3d(${position}px, 0, 0)`;
      this.swiperStyle['-webkit-transform'] = `translate3d(${position}px), 0, 0`;
      this.swiperStyle['-ms-transform'] = `translate3d(${position}px), 0, 0`;
    },
    startTimer() {
      this.timer = setInterval(() => {
        this.currentIndex++
        this.scrollSwiper(-this.currentIndex * this.imgaeWidth)
      }, this.delay)
    },
    scrollSwiper(position) {
      this.swiperStyle.transition = 'transform ' + 300 + 'ms'
      this.setTransform(position)
      this.checkPosition()
    },
    checkPosition() {
      setTimeout(() => {
        this.swiperStyle.transition = '0ms'
        if (this.currentIndex === this.count + 1) {
          this.currentIndex = 1
          this.setTransform(-this.imgaeWidth)
        } else if (this.currentIndex === 0) {
          this.currentIndex = this.count
          this.setTransform(-this.currentIndex * this.imgaeWidth)
        }
      }, 300)
    }
  }
};
</script>

<style lang="css" scoped>
.hy-swiper {
  width: 616px;
  border: 2px solid red;
  overflow: hidden;
  margin: 0 auto;
}
.swiper {
  display: flex;
}
</style>