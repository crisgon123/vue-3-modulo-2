<template>
  <div>
    <h1>Registrar pelicula</h1>
    <form @submit.prevent="enviarFormulario">
      <h3>Título y descripción de película</h3>

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
      <BaseRadioGroup
        v-model="pelicula.subtitulada"
        name="subtitulada"
        :opciones="opcionesIdioma"
      />

      <h4>{{ pelicula }}</h4>
      <h3>Idioma de subtítulos</h3>
      <div>
        <BaseCheckbox v-model="pelicula.idiomas.espanol" label="Español" />
      </div>

      <div>
        <BaseCheckbox v-model="pelicula.idiomas.ingles" label="Inglés" />
      </div>

      <button type="submit">Registrar</button>
    </form>
  </div>
</template>

<script>
export default {
  methods: {
    enviarFormulario() {
      fetch(
        "https://formulario-28ec7-default-rtdb.firebaseio.com/peliculas.json",
        {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify(this.pelicula),
        }
      );

      this.pelicula.categoria = "";
      this.pelicula.titulo = "";
      this.pelicula.descripcion = "";
      this.pelicula.subtitulada = 0;
      this.pelicula.idiomas.espanol = false;
      this.pelicula.idiomas.ingles = false;
    },
  },
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
      opcionesIdioma: [
        {
          label: "Si",
          value: 1,
        },
        {
          label: "No",
          value: 0,
        },
      ],
    };
  },
};
</script>
