<template>
  <!-- {{ App }} -->
  <div v-for="allo in App.appointment" :key="allo.id">
    <!-- {{ allo }} -->
    <Appointment :allo="allo" />
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
    emits: ["delete-Appointment", "toggle"],
  };
</script>
