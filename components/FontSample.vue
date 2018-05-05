<template>
  <div class="font-item">
    <button v-on:click="$emit('move-item', index, 0)">
      <font-awesome-icon :icon="up" />
    </button>
    {{ index }}. 
    <button v-on:click="$emit('move-item', index, -1)">
      <font-awesome-icon :icon="down" />
    </button>
    <link rel="stylesheet"
          v-bind:href="fontSource">  
    <div class="sample-text" v-bind:style="customStyle">
      <!-- <p>Files: {{ webfont.files }}</p> -->
      <slot>Sample Text</slot>
    </div>
    <div>{{ webfont.family }}</div>
  </div>
</template>

<script>
import FontAwesomeIcon from '@fortawesome/vue-fontawesome'
import faAngleDoubleUp from '@fortawesome/fontawesome-free-solid/faAngleDoubleUp'
import faAngleDoubleDown from '@fortawesome/fontawesome-free-solid/faAngleDoubleDown'

export default {
  data () {
    return {
    }
  },
  
  components: {
    FontAwesomeIcon
  },

  props: [
    'webfont',
    'index',
    'font_size'
  ],
  computed: {
    // a computed getter
    fontSource: function () {
      // `this` points to the vm instance
      return "https://fonts.googleapis.com/css?family=" + this.webfont.family.replace(' ', '+')
    },
    customStyle: function () {
      let style = "font-family: '" + this.webfont.family + "', serif; font-size: " + this.font_size + "pt;"
      //console.log(style)
      return style
    },
    up () {
      return faAngleDoubleUp
    },
    down () {
      return faAngleDoubleDown
    }

  }
}
</script>

<style>
</style>
