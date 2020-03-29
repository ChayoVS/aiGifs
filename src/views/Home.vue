<template>
  <div class="home">
    <Search></Search>
    <Footer></Footer>
  </div>
</template>

<script>
// @ is an alias to /src
import Search from '@/components/Search.vue'
import Footer from '@/components/Footer.vue'



export default {
  name: 'Home',
  components: {
    Search, 
    Footer
  }
}
</script>
