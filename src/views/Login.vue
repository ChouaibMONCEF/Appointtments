<template>
  <!-- <div class="form">
    <form class="login" action="">
      <h1>Welcome back</h1>
      <div class="Reference">
        <label for="uref">Reference</label> <br> <br>
        <input
          type="text"
          name="uref"
          id="uref"
          placeholder=" Your Reference here "
        />
      </div>
      <br>
      <Button  />
    </form>
  </div> -->


    <Login @user-Login="Login" :Ldata="Login" />
    <!-- <h1>{{data.message}}</h1> -->
    


</template>

<script>
 import Login from "../components/Login";

export default { 
    name: 'Header',
    props: {
        title: String,
        showAddUser: Boolean
    },
    components: {
        Login,
    },
    data() {
      return {
        User: [],
      };
    },
    methods: {
      async Login(user) {
        const res = await fetch("api/User/login", {
          method: "POST",
          headers: {
            "Content-type": "application/json",
          },
          body: JSON.stringify(user),
        }); 

        const data = await res.json();
        console.log(data.User);
        if(data.User.id){
        localStorage.setItem("uref",data.User.uref);
        // window.location.replace('/Home')
        this.$router.push('/')
        return data;
        }
      },
    },
    async created() {
      this.Appointment = await this.Login();
    },
  };

</script>

<style scoped>
.form {
    width: 85vw;
    display: flex;
    flex-direction: column;
    align-content: space-between;
    justify-content: space-between;
    }
.login {
    background: linear-gradient(rgb(114, 133, 216), rgb(185, 179, 240));
    margin: 50px;
    padding: 50px;
    border-radius: 20px;
}
.Reference {
    padding: 10px;
}

#uref {
    height: 40px;
    border-radius: 10px;
    border: solid 0.1px;
    width: 70%;
}

</style>
