<template>
  <div class="search">
      <h1>NASA Image Archive Search!</h1>
    <form v-on:submit.prevent="getResults(query)">
            <input type="text" placeholder="Try searching for ‘rover’✨" v-model="query" />
    </form>
    <div class="grid">
      <div
        class="image_wrap"
        v-for="(result,index) in results"
        :key="index"

        @mouseover="animateBox"
      >
        <img
          @mouseover="animateBox"
          class="grid_item"
          :src="result.links[0].href"
          :ref="`image_${index}`"
        />
        <h4>{{ result.data[0].title}}</h4> 
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { TweenMax, Power2, TimelineMax } from "gsap/TweenMax";
    

export default {
  name: "Search",
  data() {
    return {
      msg: "Search",
      query: "",
      results: "",
      title: "",
      
      // explanation: ''
    };
  },
  methods: {
    getResults(query) {
      axios
        .get(
          "https://images-api.nasa.gov/search?q=" + query + "&media_type=image" 
        )
        .then(response => {
          this.results = response.data.collection.items;         
                 });
          console.log(this.results);
    },

    animateBox() {
      TweenMax.to(
        ".grid_item",
        1.5,
        { scale: 0.95, ease: Power2.easeOut, yoyo: true },
        0.1
      );
    }
  }
};
</script>

<style scoped>
.search {
   color: --color;
  /* cursor: url("data:image/svg+xml,%3Csvg version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' x='0px' y='0px' width='52px' height='52px' viewBox='0 0 52 52' style='enable-background:new 0 0 52 52;' xml:space='preserve'%3E %3Cpath fill='%23bb3a3a' d='M29.889 30.05l-.036 21.361c-.222.213-7.654.213-7.876 0l-.007-21.358-21.52.007v-7.978l21.518.036L21.96.571h7.978l-.037 21.56 21.388.037c.213.222.213 7.654 0 7.876l-21.401.007z'/%3E %3C/svg%3E") 26 26, crosshair; */
}
h1 {
  display: block;
  position: relative;
  border: none;
  color: rgb(94, 33, 235);
  font-size: 2.5em;
  font-family: "Abel", sans-serif;
  padding-top: 8%;
  /*   margin-bottom: 1em; */
  text-align: center;
  overflow: auto;
}
img {
  width: 100%;
  height: 100%;
  display: block;
  object-fit: cover;
  border-radius: 2%;
  /* box-shadow: 5px 5px 15px 5px rgba(0, 0, 0, 0.54); */
}
.grid {
  display: grid;
  grid-gap: var(--spacing);
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  grid-auto-rows: auto;
  grid-auto-flow: dense;
  min-height: calc(100vh - var(--spacing) * 2);
  padding: 0 10% 0 10%;
  box-shadow: 5px 5px 15px 5px rgba(0, 0, 0, 0.54);
}
.grid_item {
  grid-auto-flow: column;
  top: 0;
  margin-top: 15%;
  background-size: cover;
  background-position: 50% 50%;
  /* transform: rotate(-8deg); */
  z-index: 1;
  -webkit-box-shadow: 5px 5px 15px 5px rgba(0, 0, 0, 0.54);
  box-shadow: 5px 5px 15px 5px rgba(0, 0, 0, 0.54);
}

h4 {
  font-family: "Abel", sans-serif;
  font-size: 16px;
  color: var(--color);
  z-index: 100;
  margin-top: -15%;
  transform: rotate(0deg);
  text-align: center;
  white-space: wrap;
  padding: 0 5% 0 5%

}

input {
  display: block;
  position: relative;
  border: none;
  color: red;
  font-size: 2em;
  font-family: "Abel", sans-serif;
  border-bottom: 2px solid rgb(94, 33, 235);
  padding-top: 8%;
  margin-bottom: 1em;
  width: 100%;
  height: 2.5em;
  text-align: center;
  /* vertical-align: middle; */
  background: none;
  resize: none;
  overflow: auto;
}

input:focus,
textarea:focus {
  background: rgba(0, 0, 0, 0.1);
  border-radius: 5px;
  outline: none;
  color: var(--color);
}
</style>

