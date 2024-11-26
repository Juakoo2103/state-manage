<template>
  <div :style="cardStyle" class="appointment-card">
    <h3>{{ patient }}</h3>
    <p><strong>Fecha:</strong> {{ date }}</p>
    <p><strong>Hora:</strong> {{ time }}</p>
    <p><strong>Gravedad:</strong> {{ severity }}</p>
    <p><strong>Motivo:</strong> {{ reason }}</p>
    <button @click="deleteAppointment">Eliminar</button>
  </div>
</template>

<script>
export default {
  props: {
    patient: String,
    date: String,
    time: String,
    severity: String,
    reason: String,
  },
  computed: {
    cardStyle() {
      // Colores según gravedad
      switch (this.severity) {
        case "low":
          return { backgroundColor: "green" };
        case "medium":
          return { backgroundColor: "yellow" };
        case "high":
          return { backgroundColor: "red" };
        default:
          return {};
      }
    },
  },
  methods: {
    deleteAppointment() {
      this.$emit("delete");
    },
  },
};
</script>

<style scoped>
.appointment-card {
  border: 1px solid #ddd;
  padding: 16px;
  margin-bottom: 16px;
  border-radius: 8px;
}
button {
  background-color: red;
  color: white;
  border: none;
  padding: 5px 10px;
  cursor: pointer;
}
button:hover {
  background-color: darkred;
}
</style>
