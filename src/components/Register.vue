<template>
  <form @submit="onSubmit" class="add-form">
    <div class="form-control">
      <label>FirstName</label>
      <input type="text" v-model="FirstName" name="FirstName" placeholder="" />
    </div>
    <div class="form-control">
      <label>LastName</label>
      <input type="text" v-model="LastName" name="LastName" placeholder="" />
    </div>
    <div class="form-control">
      <label>email</label>
      <input type="text" v-model="email" name="email" />
    </div>

    <input type="submit" value="Save User" class="btn btn-block" />
  </form>
</template>

<script>
  export default {
    name: "Register",
    data() {
      return {
        FirstName: "",
        LastName: "",
        email: "",
      };
    },
    methods: {
      onSubmit(e) {
        e.preventDefault();
        if (!this.FirstName) {
          alert("please add a User");
          return;
        }
        const newUser = {
          id: Math.floor(Math.random() * 100000),
          FirstName: this.FirstName,
          LastName: this.LastName,
          email: this.email,
        };
        this.$emit("add-User", newUser);
        this.FirstName = "";
        this.LastName = "";
        this.email = "";
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
