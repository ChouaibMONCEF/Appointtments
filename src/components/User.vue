<template>
  <div
    class="card"
    @dblclick="$emit('toggle-active', User.id)"
    :class="[User.active ? 'active' : '', 'User']"
  >
    <div class="inner">
      <h2>
        {{ User.name }}
        <button
          @click="$emit('delete-User', User.id)"
          class="fas fa-times"
        ></button>
      </h2>
      <h3>{{ User.email }}</h3>
    </div>
  </div>
</template>

<script>
  export default {
    name: "User",
    props: {
      User: Object,
    },
  };
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
