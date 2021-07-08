<template>
  <form @submit="onSubmit" class="add-form">
    <div class="form-control">
      <label>FirstName</label>
      <input type="text" v-model="FirstName" name="FirstName" placeholder="" />
   
      <label>LastName</label>
      <input type="text" v-model="LastName" name="LastName" placeholder="" />
    
      <label>email</label>
      <input type="text" v-model="email" name="email" />   
      
      <input type="text" hidden v-model="uref" name="uref" />
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
        uref: "",
      };
    },
    methods: {
      onSubmit(e) {
        
        e.preventDefault();
        if (!this.FirstName) {
          alert("please add a User");
          return;
        }
        function generateUref(length) {
		const characters ='ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789';
        let result = ' ';
        const charactersLength = characters.length;
        for ( let i = 0; i < length; i++ ) {
        result += characters.charAt(Math.floor(Math.random() * charactersLength));
        }
        return result;
        }
        let ref = generateUref(10);
        const newUser = {
          id: Math.floor(Math.random() * 100000),
          FirstName: this.FirstName,
          LastName: this.LastName,
          email: ref,
          uref: generateUref(10),
        };
        this.$emit("add-User", newUser);
        this.FirstName = "";
        this.LastName = "";
        this.email = "";
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
