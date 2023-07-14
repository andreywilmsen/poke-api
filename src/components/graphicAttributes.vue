<template>
  <pokedexElement @sendAttributes="dataApi" />
  <div id="graphicElement">
    <h5 data-anime="up" id="attributesTitle">Attribute stats</h5>
    <div data-anime="up" id="graphicGeneral">
      <div class="columnSection" @send="generateStats">
        <p>240</p>
        <div class="graphicColumn">

          <div id="hp" class="graphicItems">{{ stats[0] }}</div>
        </div>
        <div class="graphicText"><span>HP</span></div>
      </div>
      <div class="columnSection">
        <p>240</p>
        <div class="graphicColumn">
          <div id="attack" class="graphicItems">{{ stats[1] }}</div>
        </div>
        <div class="graphicText"><span>Attack</span></div>
      </div>
      <div class="columnSection">
        <p>240</p>
        <div class="graphicColumn">
          <div id="defense" class="graphicItems">{{ stats[2] }}</div>
        </div>
        <div class="graphicText"><span>Defense</span></div>
      </div>
      <div class="columnSection">
        <p>240</p>
        <div class="graphicColumn">
          <div id="specialAttack" class="graphicItems">{{ stats[3] }}</div>
        </div>
        <div class="graphicText"><span>Special Attack</span></div>
      </div>
      <div class="columnSection">
        <p>240</p>
        <div class="graphicColumn">
          <div id="specialDefense" class="graphicItems">{{ stats[4] }}</div>
        </div>
        <div class="graphicText"><span>Special Defense</span></div>
      </div>
      <div class="columnSection">
        <p>240</p>
        <div class="graphicColumn">
          <div id="speed" class="graphicItems">{{ stats[5] }}</div>
        </div>
        <div class="graphicText" href="#footer"><span>Speed</span></div>
      </div>
    </div>
  </div>
</template>

<script>
import pokedexElement from './pokedexElement.vue';

export default {

  name: 'graphicAttributes',
  components: {
    pokedexElement
  },
  data() {
    return {
      stats: [],
    }
  },
  methods: {

    // ANIMAÇÃO PARA APARECER O ELEMENTO NA TELA

    animeScroll: function (item) {
      const windowTop = window.pageYOffset + window.innerHeight * 0.85;
      item.forEach(element => {
        if (windowTop > element.offsetTop) {
          element.classList.add("animate");
        }
      })
    },

    // EMIT DO POKEDEXELEMENT COM OS DADOS EM JSON DO POKEMON

    dataApi: async function (data) {
      let response = data
      this.stats = [];

      // ARMAZENA VALOR DE ATRIBUTOS (attributes stats)

      for (let i = 0; i < 6; i++) {
        let arrStats = response.stats[i];
        let arrStatsFilter = Object(arrStats).base_stat
        this.stats.push(arrStatsFilter)
        await this.createGraph(this.stats[i], i);
      }

      // manipulação de template

      const item = document.querySelectorAll("[data-anime]");

      window.addEventListener("scroll", () => {
        this.animeScroll(item);
        document.querySelector('#graphicGeneral').setAttribute('data-anime', 'up')
      });
    },

    // INSERE OS ATRIBUTOS DE PODER NO GRÁFICO PARA GERAR A INTERFACE GRÁFICA 

    createGraph: async function (stat, i) {
      document.querySelector('#graphicElement').style.display = 'flex';
      let columns = document.querySelectorAll('.graphicItems')
      let reference = 0.4;
      columns[i].style.height = ``
      let result = stat * reference;

      // manipulação de template

      columns[i].style.height = `${result}%`
      columns[i].style.backgroundImage = `linear-gradient(180deg, #57fbd8 0%, #67e1f6 100%)`
      columns[i].style.transition = `2s 2s`
    }
  }
}
</script>

<style>
#graphicElement {
  display: none;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 100%;
  height: 100vh;
  background-color: rgba(255, 255, 255, 0.548);
  scroll-snap-align: start;
}

#attributesTitle {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 400px;
  height: 30px;
  margin-bottom: 30px;
  font-size: 18px;
}

#graphicGeneral {
  width: 600px;
  height: 500px;
  background-color: rgb(211, 10, 64);
  box-shadow: 1px 1px 32px 14px rgba(128, 128, 128, 0.164);
  border-radius: 8px;
  margin-bottom: 30px;
  display: flex;
  align-items: center;
  justify-content: space-around;
  color: white;
}

@media (max-width: 630px) {
  #graphicGeneral {
    width: 315px;
    height: 300px;
    font-size: 12px;
  }

  #attributesTitle {
    width: 320px;
  }
}

.columnSection {
  width: 15%;
  height: 95%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;

}

.graphicColumn {
  width: 100%;
  height: 90%;
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  border: 1px solid rgba(128, 128, 128, 0.267);
  background-color: white;
}

.graphicItems {
  width: 100%;
  height: 0%;
  color: rgb(53, 53, 53);
  font-weight: 600;
}

.graphicText {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 18%;
  text-align: center;
}

[data-anime] {
  opacity: 0;
  transition: 1.5s;
}

[data-anime="up"] {
  transform: translate3d(0, 100%, 0);
}

[data-anime].animate {
  opacity: 1;
  transform: translate3d(0, 0, 0);
}
</style>
