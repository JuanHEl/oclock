<template>
  <div class="py-4 container-fluid">
    <div v-for="(pregunta, index) in preguntas" :key="index">
      <p>Pregunta {{ index + 1 }}</p>
      <label>Texto:</label>
      <input v-model="pregunta.texto" type="text" />
      <label>Tipo:</label>
      <select v-model="pregunta.tipo">
        <option :key v-for="(opc, key) in opc_tipo" :value="opc.nombre">{{opc.salida}}</option>
      </select>
      <label>Obligatoria:</label>
      <input v-model="pregunta.obligatoria" type="checkbox" />
      <label>Icono:</label>
      <select v-model="pregunta.icono">
        <option :key v-for="(opc, key) in opc_icon" :value="opc.nombre">{{opc.salida}}</option>
      </select>
      <label v-if="pregunta.tipo === 'opciones'">Opciones:</label>
      <div v-if="pregunta.tipo === 'opciones'">
        <input v-for="(opcion, i) in pregunta.opciones" :key="i" v-model="pregunta.opciones[i]" type="text" />
        <button @click="agregarOpcion(index)">Agregar Opción</button>
      </div>
      <label v-if="pregunta.tipo === 'rango'">Rango Máximo:</label>
      <input v-if="pregunta.tipo === 'rango'" v-model="pregunta.rangoMaximo" type="number" />
      <button @click="eliminarPregunta(index)">Eliminar Pregunta</button>
    </div>
    <button @click="agregarPregunta">Agregar Pregunta</button>
    <hr />
    <button @click="guardarEstado">Guardar Estado</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      preguntas: [
        {
          texto: "",
          tipo: "rango",
          obligatoria: false,
          icono: "star",
          opciones: [],
          rangoMaximo: 5
        }
      ],
      opc_tipo:[{nombre:"rango",salida:"rango"},{nombre:"cerrado",salida:"cerrado"},{nombre:"abierto",salida:"abierto"},{nombre:"opciones",salida:"opciones"}],
      opc_icon:[{nombre:"star",salida:"Estrella"},{nombre:"smile-beam",salida:"Sonrisa"},{nombre:"user",salida:"Usuario"},{nombre:"file-signature",salida:"Firma"},{nombre:"chart-pie",salida:"Gráfico"},{nombre:"users",salida:"Usuarios"},{nombre:"comments",salida:"Comentarios"}]
    };
  },
  methods: {
    agregarPregunta() {
      this.preguntas.push({
        texto: "",
        tipo: "rango",
        obligatoria: false,
        icono: "star",
        opciones: [],
        rangoMaximo: 5
      });
    },
    eliminarPregunta(index) {
      this.preguntas.splice(index, 1);
    },
    agregarOpcion(index) {
      this.preguntas[index].opciones.push("");
    },
    guardarEstado() {
      // Aquí podrías enviar this.preguntas a tu servidor o almacenarlo localmente.
      console.log(this.preguntas);
    }
  }
};
</script>

<style scoped>
.fa-icon {
  font-family: 'Font Awesome 5 Free';
}

/* Estilos personalizados para los iconos */
.fa-icon option {
  padding-left: 20px; /* Espaciado a la izquierda para separar el icono del texto */
  background-repeat: no-repeat; /* Evitar repetición del icono */
  background-position: 3px 50%; /* Alinear el icono verticalmente */
}

/* Estilos para el texto junto al icono */
.fa-icon option::before {
  margin-right: 10px; /* Espaciado a la derecha para separar el icono del texto */
}
</style>
