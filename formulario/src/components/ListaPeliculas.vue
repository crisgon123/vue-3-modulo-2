<template>
  <div class="lista-peliculas">
    <h3 class="titulo">{{ titulo }}</h3>
    <div v-for="pelicula in peliculas" :key="pelicula.titulo" class="pelicula">
      <h4>{{ pelicula.titulo }}</h4>
      <p
        class="categoria"
        :class="{ [`categoria-${pelicula.categoria}`]: true }"
      >
        {{ pelicula.categoria.toUpperCase() }}
      </p>

      <p class="descripcion">{{ pelicula.descripcion }}</p>
      <p class="subtitulos">
        <span v-if="pelicula.subtitulada">Subtítulos: </span>
        <span v-else><i>Sin subtitulos</i></span>
        <span v-if="pelicula.subtitulada && pelicula.idiomas.espanol"
          ><i>Español </i></span
        >
        <span v-if="pelicula.subtitulada && pelicula.idiomas.ingles"
          ><i>Inglés</i></span
        >
      </p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["peliculas", "titulo"],
};
</script>

<style scoped>
.lista-peliculas {
  margin: 4rem 2rem;
}
.titulo {
  text-align: center;
}
.pelicula {
  color: whitesmoke;
  width: 80%;
  line-height: 0.7rem;
  padding: 0.1rem 1rem;
  margin: 0.5rem 0rem;
  border-radius: 10px;
  background-color: #333;
}
h4 {
  margin: 1.5rem 0rem 0.5rem;
  display: inline-block;
}

.categoria {
  padding: 0.5rem;
  float: right;
  border-radius: 5px;
  font-weight: 700;
  color: #333;
}
.categoria-thriller {
  background-color: lightsalmon;
}
.categoria-terror {
  background-color: red;
}
.categoria-comedia {
  background-color: lightseagreen;
}
.categoria-animada {
  background-color: pink;
}
.categoria-accion {
  background-color: lightgray;
}
.descripcion {
  line-height: 1.2rem;
}
.subtitulos {
  color: #bbb;
}
</style>