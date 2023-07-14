<template>
  <nav>
    <img alt="Logotipo" src="../assets/pokelog.png">
    <h2>DESENVOLVIDO POR ANDREY WILMSEN</h2>
  </nav>
</template>

<script>
export default {
  name: 'navSection',
}
</script>

<style>
nav {
  width: 100%;
  height: 80px;
  background-color: black;
  color: white;
  display: flex;
  justify-content: space-between;
  align-items: center;
  scroll-snap-align: start;
}

nav img {
  width: 130px;
  margin-left: 20px;
}

nav h2 {
  color: rgb(254, 202, 27);
  margin-right: 20px;
}



@media (max-width: 650px) {
  nav {
    height: 130px;
    align-items: space-between;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  nav img {
    height: 60px;
    margin-left: 0px;
  }

  nav h2 {
    height: 50%;
    display: flex;
    align-items: center;
    color: rgb(254, 202, 27);
    margin-right: 0px;
    text-align: center;
    font-size: 15px;
  }
}</style>
