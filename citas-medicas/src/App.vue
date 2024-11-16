<script>
import Tabla from './components/Tablas.vue';

export default {
  components: {
    Tabla,
  },
  data() {
    return {
      form: {
        paciente: '',
        fecha: '',
        hora: '',
        gravedad: '',
        motivo: '',
      },
      citas: [],
    };
  },
  computed: {
    esFormularioValido() {
      return this.form.paciente && this.form.fecha && this.form.hora && this.form.gravedad && this.form.motivo;
    },
  },
  methods: {
    agregarCita() {
      this.citas.push({ ...this.form });
      this.form.paciente = '';
      this.form.fecha = '';
      this.form.hora = '';
      this.form.gravedad = '';
      this.form.motivo = '';
    },
    eliminarCita(index) {
      this.citas.splice(index, 1);
    },
  },
};
</script>

<template>
  <div id="app">
    <h2>Administrador de Citas Médicas</h2>

    <!-- Formulario de Cita -->
    <form @submit.prevent="agregarCita">
      <div class="formulario">
        <div class="form-group">
          <label :class="{'text-danger': !form.paciente}">Paciente:</label>
          <input v-model="form.paciente" type="text" required />
        </div>

        <div class="form-group">
          <label :class="{'text-danger': !form.fecha}">Fecha:</label>
          <input v-model="form.fecha" type="date" required />
        </div>

        <div class="form-group">
          <label :class="{'text-danger': !form.hora}">Hora:</label>
          <input v-model="form.hora" type="time" required />
        </div>

        <div class="form-group">
          <label :class="{'text-danger': !form.gravedad}">Gravedad:</label>
          <select v-model="form.gravedad" required>
            <option value="">Seleccione</option>
            <option value="baja">Baja</option>
            <option value="media">Media</option>
            <option value="alta">Alta</option>
          </select>
        </div>

        <div class="form-group">
          <label :class="{'text-danger': !form.motivo}">Motivo:</label>
          <textarea v-model="form.motivo" required></textarea>
        </div>
      </div>
      
      <!-- Botón de agregar cita -->
      <button :disabled="!esFormularioValido" type="submit">Agregar</button>
    
    </form>

    <!-- Mensaje si no hay citas -->
    <p v-if="citas.length === 0" class="text-danger">No hay consultas registradas.</p>

    <!-- Mostrar las citas -->
    <div class="container">
      <div v-for="(cita, index) in citas" :key="index">
        <Tabla :cita="cita" @eliminar="eliminarCita(index)" />
      </div>
    </div>

  </div>
</template>

<style scoped>
.text-danger {
  color: red;
}

form {
  max-width: 1000px;
  margin: auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 10px;
}

.formulario {
  display: flex;
  flex-wrap: nowrap; /* Evita el salto de línea, todo en una sola fila */
  justify-content: space-between;
  gap: 15px;
}

.form-group {
  display: flex;
  flex-direction: column;
  flex: 1; /* Cada campo toma el mismo ancho */
  width: 20%;
}

label {
  margin-bottom: 5px;
}

input, select, textarea {
  padding: 8px;
  font-size: 16px;
  border-radius: 4px;
  border: 1px solid #ccc;
}

textarea {
  resize: vertical;
  height: 20px;
}

button {
  width: 15%;
  padding: 10px;
  background-color: grey;
  color: black;
  border: none;
  cursor: pointer;
  font-size: 16px;
  margin-top: 30px;
}

button:disabled {
  background-color: white;
  color: gray;
  cursor: not-allowed;
}

.container {
  display: flex;
  gap: 75px;
  justify-content: flex-start;
}

</style>
