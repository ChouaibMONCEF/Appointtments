<template>
  <!-- {{ App }} -->
  <div v-if="1==1" >
  <div v-for="allo in App.appointment" :key="allo.id">
    <!-- {{ allo }} -->
    <Appointment @deleteAppointment="$emit('deleteAppointment', allo.id)" :allo="allo" />
  </div>
  </div>
</template>

<script>
  import Appointment from "./Appointment";
  export default {
    name: "Appointments",
    props: {
      App: Array,
    },
    components: {
      Appointment,
    },
    emits: ["deleteAppointment", "toggle"],
  };
</script>
