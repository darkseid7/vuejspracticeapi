<template lang="pug">
#app
    Header
    section.section 
      nav.nav.has-shadow
        .container
          input.input.is-large(
            v-model="searchQuery" 
            type="text"
            placeholder="What do you want to listen?")
        button.button.is-success.is-large(@click="search") Search!
    
      Loader-bar(v-show="loader")
      
      .container
        p
          small {{ totalSearch }}

      .container.results 
        .columns.is-multiline
          .column.is-one-quarter(v-for="t in tracks" )
            Trackkerss(v-bind:track='t')    
               
    Footer 

</template>

<script>
import trackService from '@/services/track'
import Footer from '@/components/layout/Footer.vue'
import Header from '@/components/layout/Header.vue'
import Trackkerss from '@/components/Track.vue'
import LoaderBar from '@/components/Loader.vue'

export default {
  name: 'app',
  data () {
    return {
      searchQuery: '',
      tracks: [],
      loader: false
    }
  },
  components:{
    Footer,
    Header,
    Trackkerss,
    LoaderBar
  },
  computed: {
    totalSearch () {
      return `Found: ${this.tracks.length}`
    }
  },
  methods: {
    search () {
      if (!this.searchQuery){return}
      
      else if (this.searchQuery){   
        this.loader = true
        trackService.search(this.searchQuery)
        .then(res => {
          this.loader = false
          this.tracks = res.tracks.items
          // console.log(res)
        })}

    },

  }

}
</script>

<style lang="scss" >
 @import 'scss/main.scss';
.results {
  margin-top: 30px;
}
button.button{
  float: right;
}
</style>