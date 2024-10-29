<template>
  <div>
    <h2>Gerenciador de Filmes</h2>

    <input
      type="text"
      placeholder="Título do Filme"
      v-model="title"
    />
    <input
      type="text"
      placeholder="Diretor"
      v-model="director"
    />
    <input
      type="date"
      placeholder="Ano de Lançamento"
      v-model="year"
    />

    <button @click="handleAddMovie">Adicionar Filme</button>

    <p v-if="movies.length === 0">Nenhum filme cadastrado ainda.</p>
    <ul v-else>
      <li v-for="(movie, index) in movies" :key="index">
        {{ movie.title }} - {{ movie.director }} ({{ movie.year }})
        <button @click="handleDeleteMovie(index)">Deletar</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const title = ref('');
const director = ref('');
const year = ref('');
const movies = ref([]);

const handleAddMovie = () => {
  // Verificação de campos vazios
  if (!title.value || !director.value || !year.value) {
    alert("Por favor, preencha todos os campos.");
    return;
  }

  // Criação do novo filme e adição à lista
  const newMovie = { title: title.value, director: director.value, year: year.value };
  movies.value.push(newMovie);

  // Limpeza dos campos após cadastro
  title.value = '';
  director.value = '';
  year.value = '';
};

const handleDeleteMovie = (index) => {
  movies.value.splice(index, 1);
};
</script>

<style scoped>
/* Adicione estilos personalizados aqui, se necessário */
</style>
