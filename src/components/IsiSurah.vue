<template>
  <div>
    <li v-for="(ayatQuran,index) in ayat">
      <p>{{ ayatQuran.verse_key + ayatQuran.text_uthmani}}</p>
      <p v-html = "Arti[index].text "></p>
    </li>
  </div>
</template>
<script>
import {ref} from "vue";
import axios from "axios";

export default {
  data() {
    return {
      ayat: ref([]),
      Arti: ref([])
    }
  },
  mounted() {
    this.getAyat()
    this.getArti()
  },
  methods: {
    getAyat() {
      axios.get(`https://api.quran.com/api/v4/quran/verses/uthmani?chapter_number=${this.$route.params.id}`)
          .then((response) => {
            console.log(response)
            this.ayat = response.data.verses
          })
          .catch((err) => {
            console.log('error' + err)
          })
    },
    getArti() {
      axios.get(`https://api.quran.com/api/v4/quran/translations/33?chapter_number=${this.$route.params.id}`)
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