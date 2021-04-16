<template>
  <div>
    <Carousel />
    <MainContent />
  </div>
</template>


<script>
import Carousel from '~/components/landing/Carousel'
import MainContent from '~/components/landing/MainContent'

export default {
  components: {
    Carousel, MainContent
  },
  data(){
    return {
    }
  },
}
</script>



