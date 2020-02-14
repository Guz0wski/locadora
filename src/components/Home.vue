<template>
  <div class="home">
      <h1>Bem vindo a {{ title }}</h1>

      <h3 v-if="horas >= 7 && horas < 17" id="aberta">ABERTA</h3>
      <h3 v-else-if="horas >= 17 && horas < 18" id="proxima-fechar">PRÓXIMA DE FECHAR</h3>
      <h3 v-else id="fechada">FECHADA</h3>

      <b-row>
        <b-card-group deck>
          <b-card :key="filme.id" v-for="filme in filmes" class="sm-3"
            :img-src="filme.imagem"
            :title="filme.titulo"
            :sub-title="filme.descricao"
            style="width: 14rem"
          >
            <p>{{ filme.valor | formatarValor('R$') }}</p>
            <b-button variant="outline-primary">Alugar</b-button>
          </b-card>
        </b-card-group>
      </b-row>
  </div>
</template>

<script>
export default {
  name: 'Home',

  data: function() {
    return {
      title: 'Locadora de Filmes',
      horas: new Date().getHours(),
      filmes: [
        {id: 1, titulo: "Vingadores", descricao: "Um filme de heróis", valor: 25, imagem: "https://upload.wikimedia.org/wikipedia/pt/thumb/9/9b/Avengers_Endgame.jpg/250px-Avengers_Endgame.jpg"},
        {id: 2, titulo: "Pantera Negra", descricao: "Um filme de panteras", valor: 35, imagem: "https://upload.wikimedia.org/wikipedia/pt/9/90/Pantera_Negra_%28poster%29.jpg"},
        {id: 3, titulo: "Homem-Formiga", descricao: "Um filme de formigas", valor: 20, imagem: "https://upload.wikimedia.org/wikipedia/pt/thumb/9/90/Ant_Man-Poster.jpg/250px-Ant_Man-Poster.jpg"},
        {id: 4, titulo: "Capitã Marvel", descricao: "Um filme de capitãs", valor: 40, imagem: "https://br.web.img2.acsta.net/pictures/19/02/04/18/35/1468867.jpg"},
        {id: 5, titulo: "Hulk", descricao: "Um filme de força", valor: 10, imagem: "https://br.web.img2.acsta.net/c_215_290/pictures/210/485/21048566_20131010182211313.jpg"}
      ]
    }
  },

  filters: {
    formatarValor(valor, prefixo) {
      if (!parseInt(valor)) {
        return ""
      }

      let valorFormatado = (valor.toFixed(2)).replace('.', ',')
      return prefixo + ' ' + valorFormatado
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
#aberta {
  color: blue;
}
#proxima-fechar {
  color: orange;
}
#fechada {
  color: red;
}
</style>
