<template>
  <footer>
    <ul>
      <a href="https://github.com/andreywilmsen" target="_blank">
        <img alt="Github" src="../assets/github.png">
        <li>Github</li>
      </a>
      <a href="https://br.linkedin.com/in/andrey-wilmsen-de-paula-004b49213" target="_blank">
        <img alt="Linkedin" src="../assets/linkedin.png">
        <li>Linkedin</li>
      </a>

    </ul>
  </footer>
</template>
  
<script>
export default {
  name: 'footerSection',
}
</script>
  
<style>
footer {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100px;
  background-color: black;
  color: white;
  scroll-snap-align: end;

}

footer ul {
  display: flex;
  justify-content: space-around;
  list-style-type: none;
}

footer a {
  display: flex;
  justify-content: space-around;
  align-items: center;
  text-decoration: none;
  color: white;
}

footer a li {
  margin: 0px 10px;
}

@media (max-width: 400px) {
  footer a li {
    display: none;
  }

  footer img {
    display: flex;
    width: 40px;
    filter: invert(100%);
    margin: 0px 10px;
  }
}

footer img {
  display: flex;
  width: 40px;
  filter: invert(100%);
  margin: 0px 10px;
}
</style>
  