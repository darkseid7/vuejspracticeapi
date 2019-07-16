<template lang="pug">
  .card
    .card-image
      figure.image.is-1by1
        img(:src="track.album.images[0].url")

    .card-content
      .media
        .media-left
          figure.image.is-48x48
            img(:src="track.album.images[0].url")

        .media-content
          p.title.is-6
            strong Song: {{track.name}}
          p.subtitle.is-6 Artist: {{track.artists[0].name}}

      .content   
        .small Duration: {{ totalMinutos }}m
          nav.level
            .level-left  
              a.level-item(:href="track.external_urls.spotify" target="_blank")
                  | Follow them on Spotify
              span.icon.is-small.iconoplay(@click="selectTrack")
                img(src="https://image.flaticon.com/icons/svg/60/60813.svg")
                

</template>
<script>
export default {
  data() {
    return {
      totalMinutos:''
    };
  },
  props: {
    track: { type: Object, required: true }
  },

  methods: {

    selectTrack() {
      this.$emit("select", this.track.id)

      this.$bus.$emit("set-track", this.track)
    },
    convertir() {
      let totalMin = 0;
      totalMin = Math.round(this.track.duration_ms / 1000) / 60;
      this.totalMinutos = totalMin.toFixed(2); 
      return totalMin;
    }
  },

  mounted() {
      this.convertir();  
  },

};
</script>
<style lang="scss">
.iconoplay {
  margin-left: 2px;
}
</style>
