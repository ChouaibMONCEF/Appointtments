<template>
<!-- 

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

    <input type="submit" value="Save User" class="btn btn-block" />
  </form> -->


    
    <!-- <form @submit="onSubmit" class="register" action="">
      <h1>Create New Account</h1>
      <div class="fclass">
        <label for="FirstName">First Name</label> <br> <br>
        <input
          type="text"
          v-model="FirstName"
          name="FirstName"
          id="FirstName"
          placeholder=" Chouaib "
        />
      </div>
      <div class="fclass">
        <label for="LastName">Last Name</label> <br> <br>
        <input
          type="text"
          v-model="LastName"
          name="LastName"
          id="FirstName"
          placeholder=" Moncef "
        />
      </div>
      <div class="fclass">
        <label for="email">Email</label> <br> <br>
        <input
          type="text"
          v-model="email"
          name="email"
          id="FirstName"
          placeholder=" Choaibmoncef1@gmail.com "
        />
      </div>
      <br>
      <Button  />
    </form> -->

    <div>
      <Register @add-User="addUser" />
    </div>


</template>



    <script>
  import Register from "../components/Register";
  
  export default {
    name: "Home",
    props: {
      showAddUser: Boolean,
    },
    components: {
      Register,
    },
    data() {
      return {
        User: [],
      };
    },
    methods: {
      async addUser(user) {
        const res = await fetch("api/User/Register", {
          method: "POST",
          headers: {
            "Content-type": "application/json",
          },
          body: JSON.stringify(user),
        });

        const data = await res.json();

        this.Appointments = [...this.Appointments, data];
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
        console.log(data);
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
//   export default {
//     name: "Register",
//     data() {
//       return {
//         FirstName: "",
//         LastName: "",
//         email: false,
//       };
//     },
//     methods: {
//       onSubmit(e) {
//         e.preventDefault();
//         if (!this.FirstName) {
//           alert("please add a User");
//           return;
//         }
//         const newUser = {
//           id: Math.floor(Math.random() * 100000),
//           FirstName: this.FirstName,
//           LastName: this.LastName,
//           email: this.email,
//         };
//         this.$emit("add-User", newUser);
//         this.FirstName = "";
//         this.LastName = "";
//         this.email = false;
//       },
//     },
//   };
// </script>

<style scoped>
.form {
    width: 85vw;
    display: flex;
    flex-direction: column;
    align-content: space-between;
    justify-content: space-between;
    }
.register {
    background: linear-gradient(rgb(114, 133, 216), rgb(185, 179, 240));
    margin: 50px;
    padding: 50px;
    border-radius: 20px;
}
.fclass {
    padding: 10px;
}

#FirstName {
    height: 40px;
    border-radius: 10px;
    border: solid 0.1px;
    width: 70%;
 }

</style>