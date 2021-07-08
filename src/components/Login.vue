<template>
  <form @submit="onSubmit" class="add-form" action="Home">
    <div class="form-control">
      
      <label>Reference</label>
      <input type="text" v-model="uref" name="uref" placeholder="Your Reference" />
    
    <input type="submit" value="Save User" class="btn btn-block" />
    </div>
  </form>
</template>

<script>
  export default {
    name: "Login",
    data() {
      return {
        uref: "",
      };
    },
    methods: {
      onSubmit(e) {
        
        e.preventDefault();
        if (!this.uref) {
          alert("Enter a valid reference");
          return;
        }
        const Login = {
        
          uref: this.uref,
        };
        this.$emit("user-Login", Login);
        this.uref = "";
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