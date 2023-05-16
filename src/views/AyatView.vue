<template>
  <li v-for="(item,index) in ayat">
    {{item.verse_key+item.text_uthmani }}
    <p v-html = "Arti[index].text "></p>
    <hr>
  </li>

</template>

<script>
import {ref} from "vue";
import axios from "axios";
export default {
  data() {
    return {
      ayat: ref({}),
      Arti: ref({})
    }
  },
  mounted() {
    this.getAyat()
    this.getArti()
  },
  methods: {
    getAyat() {
      axios.get("https://api.quran.com/api/v4/quran/verses/uthmani")
          .then((respons) => {
            console.log(respons)
            this.ayat = respons.data.verses
          })
          .catch((err) => {
            console.log('error' + err)
          })
    },
    getArti() {
      axios.get("https://api.quran.com/api/v4/quran/translations/33")
          .then((respons) => {
            console.log(respons)
            this.Arti = respons.data.translations
          })
          .catch((err) => {
            console.log('error' + err)
          })
    }
  }
}

</script>

<style scoped>
li{
  list-style:node ;
  text-align: right;
}
</style>