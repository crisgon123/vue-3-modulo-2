<template>
  <div>
    <h1>Registrar pelicula</h1>
    <form>
      <h3>Título y descripción de película</h3>
      <h4>{{ pelicula }}</h4>

      <BaseInput v-model="pelicula.titulo" label="Título" type="text" />

      <BaseInput
        v-model="pelicula.descripcion"
        label="Descripción"
        type="text"
      />

      <BaseSelect
        :opciones="categorias"
        v-model="pelicula.categoria"
        label="Elegir categoría"
      />

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
        <label>Español</label>
      </div>

      <div>
        <input
          type="checkbox"
          v-model="pelicula.idiomas.ingles"
          class="field"
        />
        <label>Inglés</label>
      </div>

      <button type="submit">Registrar</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      categorias: ["terror", "comedia", "animada", "thriller", "acción"],
      pelicula: {
        categoria: "",
        titulo: "",
        descripcion: "",
        subtitulada: 0,
        idiomas: {
          espanol: false,
          ingles: false,
        },
      },
    };
  },
};
</script>
