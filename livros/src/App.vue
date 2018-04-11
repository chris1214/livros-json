<script>
export default {
  data () {
    return {
      livrosPT: [],
      livrosEN: [],
      livrosES: [],
      novoLivro: {},
      select: {},
    }
  },
  methods: {
    add() {
      if(this.novoLivro.idioma === 'PT'){
        this.livrosPT.push(this.novoLivro);
        this.novoLivro = {}
      } else if(this.novoLivro.idioma === 'EN'){
        this.livrosEN.push(this.novoLivro);
        this.novoLivro = {}
      } else if(this.novoLivro.idioma === 'ES'){
        this.livrosES.push(this.novoLivro);
        this.novoLivro = {}
      }
    },
    excluir(livro) {
      this.select = livro;
      console.log('select' + this.select)
      if(this.select.idioma === 'PT'){
         this.livrosPT.splice(this.livrosPT.indexOf(this.select), 1);
      }

      if(this.select.idioma === 'EN'){
        this.livrosEN.splice(this.livrosEN.indexOf(this.select), 1);
      }

      if(this.select.idioma === 'ES'){
        this.livrosES.splice(this.livrosES.indexOf(this.select), 1);
      }
    }
  }
}
</script>
<template>
  <div id="app">

      <h1>Livros</h1>

      <div class="create" id="create">
        <Label>Titulo</Label>
        <input placeholder="Titulo" v-model="novoLivro.title">
        <Label>Idioma</Label>
        <select placeholder="idioma" v-model="novoLivro.idioma">
          <option>PT</option>
          <option>EN</option>
          <option>ES</option>
        </select>
        <button @click="add()">Salvar</button>
      </div>

      <p style="text-align: center; margin: 10px">Tabela PT</p>
      <table style="width: 100%;text-align: left;" border="1px">
        <thead>
        <tr>
        <th>Titulo PT</th>
        <th>Idioma PT</th>
        <th></th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="livro in livrosPT">
          <td>{{livro.title}}</td>
          <td>{{livro.idioma}}</td>
          <td><button @click="excluir(livro)">Excluir</button></td>
        </tr>
        </tbody>
      </table>

      <p style="text-align: center; margin: 10px">Tabela EN</p>
      <table style="width: 100%;text-align: left;" border="1px">
        <thead>
        <tr>
          <th>Titulo EN</th>
          <th>Idioma EN</th>
          <th></th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="livro in livrosEN">
          <td>{{livro.title}}</td>
          <td>{{livro.idioma}}</td>
          <td><button @click="excluir(livro)">Excluir</button></td>
        </tr>
        </tbody>
      </table>

      <p style="text-align: center; margin: 10px">Tabela ES</p>
      <table style="width: 100%;text-align: left;" border="1px">
        <thead>
        <tr>
          <th>Titulo ES</th>
          <th>Idioma ES</th>
          <th></th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="livro in livrosES">
          <td>{{livro.title}}</td>
          <td>{{livro.idioma}}</td>
          <td><button @click="excluir(livro)">Excluir</button></td>
        </tr>
        </tbody>
      </table>
  </div>
</template>
