<template>
  <!-- {{ App }} -->
  <div v-if="1==1" >
  <div v-for="aptmnt in App.appointment" :key="aptmnt.id">
    <!-- {{ aptmnt }} -->
    <Appointment @deleteAppointment="$emit('deleteAppointment', aptmnt.id)" :aptmnt="aptmnt" />
    
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
