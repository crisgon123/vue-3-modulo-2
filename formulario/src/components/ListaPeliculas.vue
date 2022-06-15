<template>
  <div class="lista-peliculas">
    <h3 class="titulo">Últimas películas</h3>
    <div class="pelicula">
      <h4>Memento (2000)</h4>
      <p class="categoria categoria-thriller">THRILLER</p>

      <p class="descripcion">Película con desenlace inesperado</p>
      <p class="subtitulos">
        <span>Subtítulos: </span>
        <span><i>Sin subtitulos</i></span>
        <span><i>Español </i></span>
        <span><i>Inglés</i></span>
      </p>
    </div>
  </div>
</template>

<script>
export default {};
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