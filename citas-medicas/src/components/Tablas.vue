<script>
export default {
  props: {
    cita: Object,
  },
  computed: {
    colorGravedad() {
      switch (this.cita.gravedad) {
        case 'baja':
          return 'lightgreen';
        case 'media':
          return 'yellow';
        case 'alta':
          return 'red';
        default:
          return 'white';
      }
    },
  },
  methods: {
    eliminar() {
      this.$emit('eliminar');
    },
  },
};
</script>

<template>
    <div :style="{ backgroundColor: colorGravedad }" class="card">
    <p><strong>Paciente:</strong><br> {{ cita.paciente }}</p>
    <p><strong>Fecha:</strong><br> {{ cita.fecha }}</p>
    <p><strong>Hora:</strong><br> {{ cita.hora }}</p>
    <p><strong>Motivo:</strong><br> {{ cita.motivo }}</p>
    <button @click="eliminar">Eliminar</button>
  </div>
</template>
  
<style scoped>
.card {
    width: 100%;
    padding: 15px;
    margin-bottom: 10px;
    margin-top: 30px;
    border-radius: 8px;
    box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
    color: black;
}

button {
    margin-top: 10px;
    padding: 8px;
    background-color: gray;
    color: black;
    border: none;
    cursor: pointer;
    font-size: 14px;
}

button:hover {
    background-color: gray;
}
</style>