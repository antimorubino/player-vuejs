<script setup>
//import Lavori from '@/views/Lavori.vue';
//import axios from 'axios';
import { ref } from 'vue'
import $ from 'jquery'

defineProps({
  idP: String,
  titolo: String,
  src: String,
  pdf: String
})
</script>

<template>

  <div class="py-1">
    <div class="my-3" v-if="src != ''">{{ titolo }} <span v-if="pdf != ''"> - </span><a :href="'./pdf/'+pdf" target="_blank" v-if="pdf != ''">Download testi</a></div>
    <audio controls preload="auto" :src="'./audio/'+src" type="audio/mpeg" id="audio" autoplay>
      <source v-if="src != 0" :src="'/audio/'+src" />
      <!--source src="/audio/01_Awesome-God.mp3" /-->
    </audio>
  </div>

</template>

<style>

  audio {
    /*width: 100%;*/
    margin: 0 auto;
  }

</style>

<script>


//chiudi('#div1')

export default {
  name: 'Riproduci',
  methods: {
    
  }
  
}
</script>
