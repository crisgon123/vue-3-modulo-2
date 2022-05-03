<template>
  <div>
    <h1>Registrar pelicula</h1>
    <form>
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
