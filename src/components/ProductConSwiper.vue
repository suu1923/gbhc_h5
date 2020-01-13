<template>
  <div class="slider-banner product-bg">
    <swiper
      class="swiper-wrapper"
      :options="ProductConSwiper"
      v-if="imgUrls.length > 0"
    >
      <swiperSlide
        class="swiper-slide"
        v-for="item in imgUrls"
        :key="item"
        ref="goodSwiper"
      >
        <video
          :src="item"
          v-if="checkSuffix(item)"
          class="slide-image"
          controls
        ></video>
        <img :src="item" v-else class="slide-image" />
      </swiperSlide>
    </swiper>
    <div class="pages">{{ currents || 1 }}/{{ imgUrls.length || 1 }}</div>
  </div>
</template>
<script>
import { swiper, swiperSlide } from "vue-awesome-swiper";
import "@assets/css/swiper.min.css";
export default {
  name: "ProductConSwiper",
  components: {
    swiper,
    swiperSlide
  },
  props: {
    imgUrls: {
      type: Array,
      default: () => []
    }
  },
  data: function() {
    let that = this;
    return {
      currents: 1,
      ProductConSwiper: {
        // autoplay: {
        //   disableOnInteraction: false,
        //   delay: 2000
        // },
        loop: true,
        speed: 1000,
        observer: true,
        observeParents: true,
        on: {
          slideChangeTransitionStart: function() {
            that.currents = this.realIndex + 1;
          }
        }
      }
    };
  },
  mounted: function() {},
  methods: {
    checkSuffix: function(url) {
      var result = false;
      if (url.substr(url.length - 3) == "mp4") result = true;
      return result;
    }
  }
};
</script>
