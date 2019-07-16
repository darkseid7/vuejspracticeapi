<template lang="pug">
main
  section.section 
    nav.nav
      .container
        input.input.is-large(
          v-model="searchQuery" 
          type="text"
          placeholder="What do you want to listen?")
      button.button.is-success.is-large(@click="search") Search!
      
    br
    .container
      .columns
        .column.is-2
          .notification.is-info {{ totalSearch }}

    Notification(v-show="showNotification")
        h1(slot="error") Something went wrong
    
    Loader-bar(v-show="loader")

    .container.results 
      .columns.is-multiline
        .column.is-one-quarter(v-for="t in tracks" )
          Trackkerss(v-bind:track='t' @select="setSelectedTrack" v-bind:class="{ 'is-active': t.id == cancionSeleccionada }" )    
      .columns(v-show="isSuccess")
        .column.is-4.is-offset-4.has-text-centered
          .notification.is-success success        

</template>

<script>
import trackService from '@/services/track'
import Trackkerss from '@/components/Track.vue'
import LoaderBar from '@/components/Loader.vue'
import Notification from '@/components/Notification.vue'
export default {
  name: 'app',
  data () {
    return {
      cancionSeleccionada: '',
      searchQuery: '',
      tracks: [],
      loader: false,
      showNotification: false,
      isSuccess: false
    }
  },
  components:{
    Trackkerss,
    LoaderBar,
    Notification
  },
  computed: {
    totalSearch () {
      return `Found: ${this.tracks.length}`
    }
  },
  methods: {
    setSelectedTrack (id) {
      this.cancionSeleccionada = id
    },

    search () {
      if (!this.searchQuery){return}
      
      else if (this.searchQuery){   
        this.loader = true
        trackService.search(this.searchQuery)
        .then(res => {
          this.showNotification = res.tracks.total === 0
          this.loader = false
          this.isSuccess = res.tracks.total > 0
          this.tracks = res.tracks.items
       //  console.log(this.showNotification)
        })}

    }

  },

  watch: {
    showNotification() {
      if(this.showNotification){
        setTimeout(() =>  {
          this.showNotification = false
        }, 3000)
      }
  }

}
}
</script>

<style lang="scss" >
.results {
  margin-top: 30px;
}
button.button{
  float: right;
}

.is-active {
  border: 2px #23d160 solid;
 }
</style>