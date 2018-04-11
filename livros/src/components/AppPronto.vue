<script>
export default {
  data () {
    return {
      livrosPT: [],
      livrosEN: [],
      livrosES: [],
      novoLivro: {},
      title: '',
      id: '',
      selected: {},
      idiomaPesquisa: '',
      titlePesquisa: '',
      editarTitulo: '',
      editarIdioma: '',
      edit: {},
    }
  },
  methods: {
    salvarNovoLivro() {
      if(this.novoLivro.idioma === 'PT') {
        this.$http.post(`http://localhost:3000/livrosPT`, this.novoLivro).then(
          response=>{
            this.$set('novoLivro', {});
          },
          error=>{
            console.error(error)
          }
        )
      }

      if(this.novoLivro.idioma === 'EN') {
        this.$http.post(`http://localhost:3000/livrosEN`, this.novoLivro).then(
          response=>{
            this.$set('novoLivro', {});
          },
          error=>{
            console.error(error)
          }
        )
      }

      if(this.novoLivro.idioma === 'ES') {
        this.$http.post(`http://localhost:3000/livrosES`, this.novoLivro).then(
          response=>{
            this.$set('novoLivro', {});
          },
          error=>{
            console.error(error)
          }
        )
      }

    },
    createLivrosPT(){
     this.$http.get(`http://localhost:3000/livrosPT`).then(
        response=>{
          this.livrosPT = response.body;
          console.log(this.livrosPT)
        },
        error=>{
          console.error(error)
        }
      )
    },

    createLivrosEN(){
     this.$http.get(`http://localhost:3000/livrosEN`).then(
        response=>{
          this.livrosEN = response.body;
        },
        error=>{
          console.error(error)
        }
      )
    },

    createLivrosES(){
     this.$http.get(`http://localhost:3000/livrosES`).then(
        response=>{
          this.livrosES = response.body;
        },
        error=>{
          console.error(error)
        }
      )
    },

    excluirLivro(livro) {
      this.selected=livro;

      if(this.selected.idioma === 'PT') {
        this.$http.delete(`/livrosPT/${this.selected.id}`,this.livros).then(
          response=>{
            console.log("Delete")
          },
          error=>{
            console.log(error)
          }
        )
      }

      if(this.selected.idioma === 'EN') {
        this.$http.delete(`/livrosEN/${this.selected.id}`,this.livros).then(
          response=>{
            console.log("Delete")
          },
          error=>{
            console.log(error)
          }
        )
      }

      if(this.selected.idioma === 'ES') {
        this.$http.delete(`/livrosES/${this.selected.id}`,this.livros).then(
          response=>{
            console.log("Delete")
          },
          error=>{
            console.log(error)
          }
        )
      }
    },
  },
   created(){
    this.createLivrosPT(),
    this.createLivrosEN(),
    this.createLivrosES()
  },
}
</script>
<template>
  <div id="app">

      <h1>Livros</h1>
    <!--<div class="pesquisa" id="pesquisa">
      <h4>Pesquisa</h4>
      <input v-model="titlePesquisa" placeholder="titulo">
      <select placeholder="idiomaPesquisa" v-model="idiomaPesquisa">
        <option>PT</option>
        <option>EN</option>
        <option>ES</option>
      </select>
      <button @click="pesquisaLivro()">Pesquisar</button>
    </div>-->


      <div class="create" id="create">
        <Label>Titulo</Label>
        <input placeholder="Titulo" v-model="novoLivro.title">
        <Label>Idioma</Label>
        <select placeholder="Idioma" v-model="novoLivro.idioma">
          <option>PT</option>
          <option>EN</option>
          <option>ES</option>
        </select>
        <button @click="salvarNovoLivro()">Salvar</button>
      </div>

      <!--<div class="editar" id="editar">
        <input v-model="selected.title" placeholder="id">
        <select placeholder="Idioma" v-model="selected.idioma">
          <option>PT</option>
          <option>EN</option>
          <option>ES</option>
        </select>
        <button @click="salvarEdicao()">Editar</button>

      </div>-->

      <table style="width: 100%;text-align: left;">
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
          <td><button @click="excluirLivro(livro)">Excluir</button></td>
        </tr>
        </tbody>
      </table>

      <table style="width: 100%;text-align: left;">
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
          <td><button @click="excluirLivro(livro)">Excluir</button></td>
        </tr>
        </tbody>
      </table>
      <table style="width: 100%;text-align: left;">
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
          <td><button @click="excluirLivro(livro)">Excluir</button></td>
        </tr>
        </tbody>
      </table>
  </div>
</template>
