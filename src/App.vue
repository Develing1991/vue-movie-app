<template>
  <Header />
  <RouterView />
  <Footer />
</template>

<script>
import Header from './components/Header.vue'
import Footer from '~/components/Footer'
export default {
  components:{
    Header,
    Footer,
  }
}
</script>


