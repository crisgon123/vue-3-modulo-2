<template>
  <div class="row">
    <div class="column registro">
      <h1>Registrar pelicula</h1>
      <form @submit.prevent="enviarFormulario">
        <fieldset>
          <legend>Información de película</legend>

          <BaseInput
            v-model="pelicula.titulo"
            label="Título"
            type="text"
            :error="errores.titulo"
            @blur="validarFormato($event)"
          />

          <BaseInput
            v-model="pelicula.descripcion"
            label="Descripción"
            type="text"
            :error="errores.descripcion"
            @input="validarLongitud"
          />

          <BaseSelect
            :opciones="categorias"
            v-model="pelicula.categoria"
            label="Elegir categoría"
            :error="errores.categoria"
          />
        </fieldset>

        <fieldset>
          <legend>Subtítulos</legend>
          <h4>Disponibles</h4>
          <BaseRadioGroup
            v-model="pelicula.subtitulada"
            name="subtitulada"
            :opciones="opcionesIdioma"
          />

          <h4>Idioma</h4>
          <div>
            <BaseCheckbox v-model="pelicula.idiomas.espanol" label="Español" />
          </div>

          <div>
            <BaseCheckbox v-model="pelicula.idiomas.ingles" label="Inglés" />
          </div>
        </fieldset>

        <button type="submit">Registrar</button>
      </form>
    </div>

    <div class="column lista">
      <ListaPeliculas
        :peliculas="ultimasPeliculas"
        titulo="Últimas películas"
      />
    </div>
  </div>
</template>

<script>
import ListaPeliculas from "../components/ListaPeliculas.vue";
import axios from "axios";
export default {
  components: { ListaPeliculas },
  created() {
    this.obtenerUltimasPeliculas();
  },
  methods: {
    obtenerUltimasPeliculas() {
      axios
        .get(
          "https://formulario-28ec7-default-rtdb.firebaseio.com/peliculas.json"
        )
        .then(({ data }) => {
          this.ultimasPeliculas = data;
        })
        .catch((err) => {
          console.log("Error: ", err);
        });
    },
    validarFormato(event) {
      const re = /\S+\ \([0-9]{4}\)/;
      const valido = re.test(event.target.value);
      !valido
        ? (this.errores.titulo = "Debe llevar el año. Ej. El aro (2003)")
        : (this.errores.titulo = null);
    },
    validarLongitud() {
      setTimeout(() => {
        if (this.pelicula.descripcion.length == 0)
          this.errores.descripcion = "La descripción no puede estar en blanco";
        else if (this.pelicula.descripcion.length < 40)
          this.errores.descripcion = null;
        else this.errores.descripcion = "No puede tener más de 40 caracteres";
      }, 20);
    },
    validarFormulario() {
      // if (
      //   this.pelicula.categoria === "" ||
      //   this.pelicula.titulo === "" ||
      //   this.pelicula.descripcion === ""
      // )
      //   return false;
      // else return true;
      const errores = {};
      if (!this.pelicula.categoria)
        errores.categoria = "Debes elegir una categoría";
      if (!this.pelicula.titulo)
        errores.titulo = "El título no puede estar en blanco";
      if (!this.pelicula.descripcion)
        errores.descripcion = "La descripción no puede estar en blanco";
      this.errores = { ...this.errores, ...errores };

      const esValido = Object.values(this.errores).every(
        (x) => x === null || x === ""
      );
      return esValido;
    },
    enviarFormulario() {
      if (this.validarFormulario()) {
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
      } else {
        console.log("el formulario es inválido");
      }
    },
  },
  data() {
    return {
      ultimasPeliculas: null,
      categorias: ["terror", "comedia", "animada", "thriller", "accion"],
      errores: {
        categoria: null,
        titulo: null,
        descripcion: null,
      },
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

<style>
fieldset {
  border: 0;
  margin: 0;
  padding: 0;
}

legend {
  font-size: 27px;
  font-weight: 700;
  margin-top: 20px;
}
body {
  font-family: "Open Sans";
}

.row::after {
  content: "";
  display: table;
  clear: both;
}

.column {
  float: left;
}

.registro {
  width: 45%;
}

.lista {
  width: 55%;
}

@media screen and (max-width: 1000px) {
  .column {
    width: 100%;
  }
  .formulario {
    width: 80%;
  }
  .lista {
    width: 100vw;
  }
}
</style>