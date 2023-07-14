<template>
  <main id="generalContent">
    <graphicAttributes/>
  </main>
</template>
  
<script>
import graphicAttributes from './graphicAttributes.vue';



export default {
  name: 'mainSection',
  components: {
     graphicAttributes
  }
}
</script>
  
<style>
main {
  width: 100%;
  height: 100%;
  background: linear-gradient(to bottom, #6ab7f5, #fff);  
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>