<template>
  <form>
    <input id="inputArea" type="text"  placeholder="ID ou Nome do Pokemon" autocomplete="off">
    <button @click="dataApi" type="submit"><img src="../assets/lupa.png"></button>
  </form>
</template>
  
<script>

export default {
  name: 'formSearch',

  methods: {

    // CONEXÃO COM API

    dataApi: async function (e) {
      e.preventDefault()
      let dataFinded = '';
      let searchResult = document.querySelector('#inputArea');
      let dataInput = document.querySelector('#inputArea').value.toLowerCase();

      // VALIDAÇÃO DE PESQUISA DO INPUT

      let response = await fetch(`https://pokeapi.co/api/v2/pokemon/${dataInput}`)
      response = response.status

      if ( response === 404) {
        searchResult.value = ""
        searchResult.placeholder = "Not found"
        searchResult.style.border = '2px solid red'
        searchResult.style.transition = '1s';
        }

      // EXECUÇÃO SE PASSAR

      else {
        await fetch(`https://pokeapi.co/api/v2/pokemon/${dataInput}`)
          .then(data => {
            return data.json()
          })
          .then(dataJson => {
            dataFinded = dataJson
          }).catch(err => {
            console.log(err)
          })
        
        searchResult.style.border = '2px solid green'
        searchResult.style.transition = '1s';
        this.$emit('send', dataFinded);
      }
    },
  }
}
</script>
  
<style>
#validation {
  width: 320px;
  height: 40px;
  display: flex;
  justify-content: space-around;
  align-items: center;
  background-color: white;
}

form {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100px;
}

form input {
  width: 280px;
  height: 40px;
  margin-left: 5px;
  border-radius: 5px 0px 0px 5px;
  border: 1px solid white;
  box-shadow: 5px 5px 15px 4px rgba(128, 128, 128, 0.759);
  text-align: center;
  font-size: 18px;
}

@media (max-width: 400px) {
  form input {
    width: 230px;
    font-size: 15px;
  }
}

form button {
  width: 40px;
  height: 42px;
  border: 1px solid transparent;
  border-radius: 0px 5px 5px 0px;
  background-color: black;
  margin-right: 5px;
  box-shadow: 5px 5px 15px 4px rgba(128, 128, 128, 0.759);

}

form button img {
  width: 20px;
  filter: invert(100%);
}
</style>
  