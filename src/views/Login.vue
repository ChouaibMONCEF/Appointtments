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


    <Login @user-Login="Login" />
    


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
        console.log(data);
        return data;
      },
      async deleteUser(id) {
        if (confirm("are you sure?")) {
          const res = await fetch(`api/Appointments/${id}`, {
            method: "DELETE",
          });

          res.status === 200
            ? (this.Appointments = this.Appointments.filter(
                (User) => User.id !== id
              ))
            : alert("error deleting user");
        }
      },
      async toggleActive(id) {
        const usertoggle = await this.fetchUser(id);
        const updateuser = { ...usertoggle, active: !usertoggle.active };

        const res = await fetch(`api/Appointments/${id}`, {
          method: "PUT",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify(updateuser),
        });

        const data = await res.json();

        this.Appointments = this.Appointments.map((User) =>
          User.id === id ? { ...User, active: data.active } : User
        );
      },
      async fetchAppointments() {
        const res = await fetch("api/Appointement/getUserAppointement/2");

        const data = await res.json();
        return data;
      },
      async fetchUser(id) {
        const res = await fetch(`api/Appointments/${id}`);

        const data = await res.json();
        console.log(data);
        return data;
      },
    },

    async created() {
      this.Appointment = await this.fetchAppointments();
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
