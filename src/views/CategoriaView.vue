<script>
import axios from "axios";
import CategoriaApi from "@/Api/Categoria.js";
const categoriaApi = new CategoriaApi ();

export default{
  
  data() {
    return { 
      categoria: {},
      categorias: [],
    };
  },
  async created(){
    const categoria = await axios.get("http://localhost:4000/categories");  
  },

  methods: {
    async salvar() {
      const categoria = {
        nome: this.categoria,
      };
      const categoria_criado = await axios.post("http://localhost:4000/categories", categoria);
      this.categorias.push(categoria_criado.data);
      this.categoria = "";
    },

    async excluir(categoria) {
      await axios.delete('http://localhost:4000/categories/$ (categoria.id)')
      const indice = this.categorias.indexOf(categoria);
      this.categorias.splice(indice, 1);
    },
  },
};
</script>

<template>
  <div class="container">
    <div class="title">
      <h2>Categoria</h2>
    </div>
    <div class="form-input">
      <input type="text" placeholder="Categoria" v-model="categoria.nome" @keyup.enter="salvar" />
      <button @click="salvar">Adicionar</button>
    </div>
    <div class="list-jogadores">
      <table>
        <thead>
          <tr>
            <th>ID</th>
            <th>Categoria</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="livro in categorias" :key="livro.id">
            <td>{{ livro.id }}</td>
            <td>{{ livro.nome }}</td>
            <td>
              <button @click="alerta">Editar</button>
              <button @click="excluir">excluir</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<style scoped></style>
