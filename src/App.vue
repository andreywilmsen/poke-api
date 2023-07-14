<template>
  <navSection/>
  <mainSection/>
  <footerSection/>
</template>

<script>
import navSection from './components/nav.vue';
import footerSection from './components/footer.vue';
import mainSection from './components/main.vue';



export default {
  name: 'App',
  components: {
    navSection, footerSection, mainSection
  }
}
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Oxanium:wght@200;300;400;500;600;700&display=swap');
*{
  margin: 0;
  padding: 0;
  font-family: 'Oxanium', cursive;
}
html{
  font-family: Arial, Helvetica, sans-serif;
  scroll-behavior: smooth;
  scroll-snap-type: y;
  scroll-snap-type: y proximity;
}
body{
  margin: 0;
  padding: 0;
}
</style>
