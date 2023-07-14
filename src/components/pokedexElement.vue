<template>
  <div id="firstElement">
    <formSearch @send="extractedData" />
    <div id="card">
      <div id="subCard1">
        <img>
      </div>
      <div id="subCard2">
        <div class="cardApresentation">
          <h5 v-if="name != ``">ID: #{{ id }}</h5>
          <h3 v-if="name != ``">Name: {{ name }}</h3>
        </div>
        <div id="descriptions">
          <div v-if="name != ``" class="descriptionsItem">
            <p>Type: </p><span>{{ element }}</span>
          </div>
          <div v-if="name != ``" class="descriptionsItem">
            <p>Height: </p><span>{{ height }} m</span>
          </div>
          <div v-if="name != ``" class="descriptionsItem">
            <p>Weight: </p><span>{{ weight }} kg</span>
          </div>
          <div v-if="name != ``" class="descriptionsItem">
            <p>Abilities: </p><span>{{ abilities }}</span>
          </div>
        </div>

      </div>
    </div>
    <a v-if="name != ``" id="anchorButton" href="#graphicElement">
      <p>STATS</p>
      <p>⇩</p>
    </a>
  </div>
</template>
  
<script>
import formSearch from './formSearch.vue';


export default {

  name: 'pokedexElement',
  emits: ["sendAttributes"],
  data() {
    return {
      name: '',
      id: '',
      element: '',
      picture: '',
      height: '',
      weight: '',
      category: '',
      abilities: '',
    }
  },
  components: {
    formSearch
  },
  methods: {

    // RETORNO DA CONEXÃO DA API COM OS DADOS EM JSON DO POKEMON SOLICITADO NO INPUT "formSearch.vue"

    extractedData(data) {
      this.$emit('sendAttributes', data);

      // BLOCO DE CÓDIGO RESPONSÁVEL POR ATUALIZAR OS DADOS DO DATA() E POPULAR O HTML COM VARIÁVEIS

      this.name = (data.name).toUpperCase();
      this.id = data.id;
      this.element = (data.types[0].type.name).toUpperCase()
      this.picture = data["sprites"]["versions"]["generation-v"]["black-white"]["animated"]["front_default"]

      document.querySelector('#subCard1').children[0].src = this.picture;
      document.querySelector('#subCard1').children[0].alt = "Pokemon";

      if (data.height < 10) {
        this.height = `0.${data.height}`
      } else {
        this.height = data.height
      }

      this.weight = data.weight
      this.category = data.height
      this.abilities = (data.abilities[0].ability.name).toUpperCase()
    },
  }
}
</script>
  
<style>
#firstElement {
  width: 100%;
  min-height: 600px;
  height: 90vh;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

#card {
  margin: 20px 0px;
  width: 300px;
  height: 450px;
  background-image: url('../assets/pokedex.png');
  background-size: cover;
  border-radius: 8px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  box-shadow: 1px 1px 32px 14px rgba(128, 128, 128, 0.123);
}

#subCard1,
#subCard2 {
  margin: 4px auto;
  width: 90%;
}

#subCard1 {
  width: 75%;
  margin: 90px 20px 0px 0px;
  display: flex;
  justify-content: center;
  align-items: center;
  color: white;
  background-size: cover;
  border-radius: 15px;
  height: 45%;
}

#subCard1 img {
  width: 80px;
  color: black;
}

#subCard2 {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-direction: column;
  background-color: white;
  border: 1px solid #333;
  width: 73%;
  border-radius: 15px;
  height: 30%;
  margin: 0px 26px 25px 0px;
  box-shadow: -3px 4px 0 #888, -5px 7px 0 #333;
}

.cardApresentation {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  height: 30px;
  background-color: black;
  border: 1px solid #333;
  color: white;
  border-radius: 15px 10px 0px 0px;
}

.cardApresentation h5 {
  display: flex;
  align-items: center;
  margin-left: 10px;
  height: 100%;
  width: 30%;
  font-weight: 400;
  font-size: 15px;
}

.cardApresentation h3 {
  display: flex;
  align-items: center;
  width: 70%;
  height: 100%;
  font-weight: 400;
  font-size: 15px;
}

#descriptions {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
}

.descriptionsItem {
  width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  background-color: rgba(128, 128, 128, 0.171);
}

#descriptions p {
  display: flex;
  justify-content: flex-start;
  width: 40%;
  font-weight: 600;
}

#descriptions span {
  display: flex;
  justify-content: center;
  width: 50%;
  font-weight: 400;
}

@keyframes resizing {
  0% {
    transform: scale(1, 1);
  }

  50% {
    transform: scale(1.05, 1.05);
  }

  100% {
    transform: scale(1, 1);
  }
}

#anchorButton {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  color: white;
  font-weight: 600;
  position: absolute;
  bottom: 20px;
  right: 10px;
  background-image: linear-gradient(to bottom, rgb(211, 10, 64) 0%, rgb(238, 12, 72) 100%);
  box-shadow: 1px 1px 12px 2px rgba(128, 128, 128, 0.726);
  transform: scale(1.09, 1.09);
  animation: resizing 2s infinite;
  text-decoration: none;
}

@media (max-width: 600px) {
  #anchorButton {
    display: none;
  }
}
</style>