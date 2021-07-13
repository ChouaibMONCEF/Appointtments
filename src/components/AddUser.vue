<template>
  <form @submit="onSubmit" class="add-form">
    <div class="form-control">
      <label>Date</label>
      <input type="date" v-model="date" name="date" placeholder="" />
    </div>
    <div class="form-control">
      <label>Subject</label>
      <input type="text" v-model="subject" name="subject" placeholder="" />
    </div>
    <div class="form-control form-control-check">
      <label>Active Reminder</label>
      <input type="checkbox" v-model="reminder" name="reminder" />
    </div>
    
      <input type="text" hidden v-model="rref" name="rref" />

    <input type="submit" value="Save User" class="btn btn-block" />
  </form>
</template>

<script>
  export default {
    name: "Add User",
    data() {
      return {
        date: "",
        subject: "",
        reminder: false,
        rref: localStorage.getItem("uref"),
      };
    },
    methods: {
      onSubmit(e) {
        e.preventDefault();
        if (!this.date) {
          alert("please add a User");
          return;
        }
        const newUser = {
          id: Math.floor(Math.random() * 100000),
          date: this.date,
          subject: this.subject,
          reminder: this.reminder,
          rref: localStorage.getItem("uref"),
        };
        this.$emit("add-User", newUser);
        this.date = "";
        this.subject = "";
        this.reminder = false;
        this.rref = "";
      },
    },
  };
</script>

<style scoped>
  .add-form {
    margin-bottom: 40px;
  }
  .form-control {
    margin: 20px 0;
  }
  .form-control label {
    display: block;
  }
  .form-control input {
    width: 100%;
    height: 40px;
    margin: 5px;
    padding: 3px 7px;
    font-size: 17px;
  }
  .form-control-check {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .form-control-check label {
    flex: 1;
  }
  .form-control-check input {
    flex: 2;
    height: 20px;
  }
</style>
