<template>
  <div class="app">
    <Header/>
    <div class="container mx-auto px-4">
      <Characters/>
      <Footer/>
    </div>
  </div>
</template>

<script>
import Header from '@/components/ui/Header'
import Footer from '@/components/ui/Footer'
import Characters from '@/components/characters/Characters'
export default {
  name: 'App',
  components: {
    Header,
    Footer,
    Characters
  }
}
</script>

<style>
</style>
