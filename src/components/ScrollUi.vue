<template>
  <div class="grid">
    <div class="grid_item grid_item--slide">
      <div v-scroll="onScroll" class="image_wrap" v-for="(image, index) in images" :key="index">
        <img class="gallery_image" @mouseover="animateBox" :src="image.url">
        <h1 class="title">{{image.title}}</h1>
      </div>
    </div>
  </div>
</template>

<script>
import { TweenMax, Power2, Sine, TimelineMax } from "gsap/TweenMax";

export default {
  name: "ScrollUi",
  props: {},
  data() {
    return {
      images: [
        {
          url:
            "https://images.unsplash.com/photo-1528791067602-aee628b626fb?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=500&q=60",
          title: "Red Dress"
        },

        {
          url:
            "https://images.unsplash.com/photo-1509631179647-0177331693ae?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=700&q=60",
          title: "Trousers"
        },
        {
          url:
            "https://images.unsplash.com/photo-1544790758-5c3d7d7d360d?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60",
          title: "Shopping"
        },
        {
          url:
            "https://images.unsplash.com/photo-1550402537-6f7b6189b3b6?ixlib=rb-1.2.1&auto=format&fit=crop&w=334&q=80",
          title: "Festivals"
        }
      ],
      scrollPosition: 0
    };
  },
  computed: {
    styledGallery() {}
  },
  methods: {
    onScroll() {
      TweenMax.to(
        ".grid_item",
        3.5,
        { x: 200, ease: Power2.easeOut, rotation: 8, yoyo: false },
        0.5
      );
    },
    animateBox() {
       TweenMax.to(
        ".grid_item",
        1.5,
        { scale: 1.05, ease: Sine.easeOut, yoyo: true },
        0.5
      );
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.grid {
  display: grid;
  place-items: center;
  width: 100%;
  height: 100%;
  cursor: url("data:image/svg+xml,%3Csvg version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' x='0px' y='0px' width='52px' height='52px' viewBox='0 0 52 52' style='enable-background:new 0 0 52 52;' xml:space='preserve'%3E %3Cpath fill='%23bb3a3a' d='M29.889 30.05l-.036 21.361c-.222.213-7.654.213-7.876 0l-.007-21.358-21.52.007v-7.978l21.518.036L21.96.571h7.978l-.037 21.56 21.388.037c.213.222.213 7.654 0 7.876l-21.401.007z'/%3E %3C/svg%3E") 26 26, crosshair;
}
.img-wrap {
  width: 100%; 
  }
  .gallery_image {
  width: 50%;
  height: 50%;
  top: 0;
  margin-top: 15%;
  background-size: cover;
  background-position: 50% 50%;
  transform: rotate(-8deg);
  z-index: 1;
  -webkit-box-shadow: 5px 5px 15px 5px rgba(0, 0, 0, 0.54);
  box-shadow: 5px 5px 15px 5px rgba(0, 0, 0, 0.54);
}

.title {
  color: #fff;
  z-index: 100;
  margin-top: -13%;
  padding-bottom: 3%;
  transform: rotate(-8deg);
}
</style>
