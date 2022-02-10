<template>
  <div>
    <h1>Registrar pelicula</h1>
    <form>
      <h3>Título y descripción de película</h3>
      <label>Título</label>
      <input
        v-model="pelicula.titulo"
        type="text"
        placeholder="Título"
        class="field"
      >

      <label>Descripcion</label>
      <input
        v-model="pelicula.descripcion"
        type="text"
        placeholder="Descripción"
        class="field"
      />

      <label>Elegir categoría</label>
      <select v-model="pelicula.categoria">
        <option
          v-for="categoria in categorias"
          :value="categoria"
          :key="categoria"
          :selected="categoria === pelicula.categoria"
        >{{ categoria }}</option>
      </select>

     <h3>Película subtitulada</h3>
      <div>
        <input
            type="radio"
            v-model="pelicula.subtitulada"
            :value="1"
            name="subtitulada"
          />
        <label>Si</label>
      </div>

      <div>
        <input
          type="radio"
          v-model="pelicula.subtitulada"
          :value="0"
          name="subtitulada"
        />
        <label>No</label>
      </div>

      <h3>Idioma de subtítulos</h3>
      <div>
        <input
          type="checkbox"
          v-model="pelicula.idiomas.espanol"
          class="field"
        />
        <label>Inglés</label>
      </div>

      <div>
        <input
          type="checkbox"
          v-model="pelicula.idiomas.ingles"
          class="field"
        />
        <label>Español</label>
      </div>

      <button type="submit">Registrar</button>
    </form>

  </div>
</template>

<script>
export default {
  data () {
    return {
      categorias: [
        'terror',
        'comedia',
        'animada',
        'thriller',
        'acción'
      ],
      pelicula: {
        categoria: '',
        titulo: '',
        descripcion: '',
        subtitulada: 0,
        idiomas: {
          espanol: false,
          ingles: false
        }
      }
    }
  }
}
</script>
