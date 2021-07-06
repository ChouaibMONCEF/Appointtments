<template>
  <div
    class="card"
    @dblclick="$emit('toggle-active', allo.id)"
    :class="[allo.reminder ? 'active' : '', 'User']"
  >
    <div class="inner">
      <h2>{{ allo.date }}</h2>
        <button
          @click="$emit('delete-User', allo.id)"
          class="fas fa-times"
        ></button>
      
      <h3>{{ allo.subject }}</h3>
    </div>
  </div>
</template>

<script>
  export default {
    name: "Appointment",
    props: {
      allo: Object,
    },
  };
  console.log();
</script>

<style scoped>
  .active {
    color: Green;
  }
  .card {
    background-color: rgb(246, 225, 225);
    margin-top: 30px;
    width: 80vw;
    height: 15vh;
    border-radius: 10px;
  }
  .inner {
    padding: 20px 20px 20px 20px;
  }

  .fas {
    color: red;
  }
  .task {
    background: #f4f4f4;
    margin: 5px;
    padding: 10px 20px;
    cursor: pointer;
  }
  .task.active {
    border-left: 5px solid green;
  }
  .task h3 {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
</style>
