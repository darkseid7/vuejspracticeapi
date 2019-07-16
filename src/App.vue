<template lang="pug">
#app
  Header

  router-view

  Footer 

</template>

<script>

import Footer from '@/components/layout/Footer.vue'
import Header from '@/components/layout/Header.vue'

export default {
  name: 'app',
  data () {
    return {

    }
  },

  components: {
    Footer,
    Header
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

.is-active {
  border: 2px #23d160 solid;
 }
</style>