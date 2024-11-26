<template>
  <div>
    <!-- Formulario -->
    <form @submit.prevent="addAppointment">
      <div>
        <label :class="{ 'text-danger': !patient }" for="patient"
          >Paciente</label
        >
        <input v-model="patient" type="text" id="patient" />
      </div>
      <div>
        <label :class="{ 'text-danger': !date }" for="date">Fecha</label>
        <input v-model="date" type="date" id="date" />
      </div>
      <div>
        <label :class="{ 'text-danger': !time }" for="time">Hora</label>
        <input v-model="time" type="time" id="time" />
      </div>
      <div>
        <label :class="{ 'text-danger': !severity }" for="severity"
          >Gravedad</label
        >
        <select v-model="severity" id="severity">
          <option value="">Selecciona gravedad</option>
          <option value="low">Baja</option>
          <option value="medium">Media</option>
          <option value="high">Alta</option>
        </select>
      </div>
      <div>
        <label :class="{ 'text-danger': !reason }" for="reason">Motivo</label>
        <input v-model="reason" type="text" id="reason" />
      </div>
      <button :disabled="!isFormValid" type="submit">Agregar</button>
    </form>

    <!-- Mensaje si no hay citas -->
    <p v-if="appointments.length === 0">Aún no hay consultas registradas</p>

    <!-- Lista de citas -->
    <div v-for="(appointment, index) in appointments" :key="index">
      <AppointmentCard
        :patient="appointment.patient"
        :date="appointment.date"
        :time="appointment.time"
        :severity="appointment.severity"
        :reason="appointment.reason"
        @delete="removeAppointment(index)"
      />
    </div>
  </div>
</template>

<script>
import AppointmentCard from "./components/AppointmentCard.vue";

export default {
  components: {
    AppointmentCard,
  },
  data() {
    return {
      patient: "",
      date: "",
      time: "",
      severity: "",
      reason: "",
      appointments: [],
    };
  },
  computed: {
    isFormValid() {
      return (
        this.patient && this.date && this.time && this.severity && this.reason
      );
    },
  },
  methods: {
    addAppointment() {
      const newAppointment = {
        patient: this.patient,
        date: this.date,
        time: this.time,
        severity: this.severity,
        reason: this.reason,
      };
      this.appointments.push(newAppointment);

      // Limpiar formulario
      this.patient = "";
      this.date = "";
      this.time = "";
      this.severity = "";
      this.reason = "";
    },
    removeAppointment(index) {
      this.appointments.splice(index, 1);
    },
  },
};
</script>

<style scoped>
.text-danger {
  color: red;
}
</style>
