<template>
  <section class="container">
      <!--
      <h1 class="title">
        font-sorter
      </h1>
      <h2 class="subtitle">
        Easily pick your favorite web fonts for a project
      </h2>

      <div>
        Error: {{ error }}
      </div>
      <div>
        Fonts: {{ fonts }}
      </div>

      // didn't get this one working:
      <font-sample v-for="family in fonts" v-bind:family="family"></font-sample>
      -->
    <div >
      <input v-model="sample" placeholder="edit me">
      <input v-model="font_size" placeholder="14">

      
      <draggable v-model="fonts" @start="drag=true" @end="drag=false" class="all-fonts">
        <font-sample
           v-for="(webfont, index) in fonts"
           :key="webfont.family"
           :webfont="webfont"
           :index="index"
           :font_size="font_size"
           v-on:move-item="onMoveItem"
           >{{ sample }}</font-sample>
      </draggable>
    </div>
      <!--
      <ul>
        <li
           is="font-sample"
           v-for="family in fonts"
           v-bind:key="family.family"
           v-bind:webfont="family"
           ></li>
      </ul>
      <div class="links">
        <a
          href="https://nuxtjs.org/"
          target="_blank"
          class="button--green">Documentation</a>
        <a
          href="https://github.com/nuxt/nuxt.js"
          target="_blank"
          class="button--grey">GitHub</a>
      </div>
      -->
  </section>
</template>

<script>
import axios from 'axios'
import draggable from 'vuedraggable'
import FontSample from '~/components/FontSample.vue'
// import AppLogo from '~/components/AppLogo.vue'

export default {
  data () {
    return {
      loading: false,
      fonts: [  ],
      // http://clagnut.com/blog/2380/
      // https://en.wikipedia.org/wiki/The_quick_brown_fox_jumps_over_the_lazy_dog
      // The quick brown fox jumps over the lazy dog
      sample: 'The five boxing wizards jump quickly.',
      font_size: '16',
      error: null
    }
  },
  components: {
    draggable,
    FontSample
  },

  created () {
    // fetch the data when the view is created and the data is
    // already being observed
    this.fetchData()
  },

  methods: {
    onMoveItem (index, destination) {
      console.log(index, destination)
    },
    
    fetchData () {
      //console.log(this.post)
      this.loading = true
      axios.get('https://www.googleapis.com/webfonts/v1/webfonts?key=AIzaSyBx7rQumhCDeLW9kdamvr82A6k3tA92a6Y')
        .then((response) => {
          this.loading = false
          //console.log(response)
          this.fonts = response.data.items;
        })
        .catch((error) => {
          this.error = error.toString();
        });
    }
  }
}
</script>

<style>

.all-fonts {
  display: flex;
  flex-wrap: wrap;
}

.font-item {
  flex: 1 1 250px;
  margin-bottom: 10px;

}
  
.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
