<template>
  <div v-show="showAddUser">
    <AddUser @add-User="addUser" />
  </div>
  <!-- CUSTOM EVENT LISTENER -->
  <Appointments
    @toggle="toggleActive"
    @delete-User="deleteUser"
    :App="Appointment"
  />
</template>

<script>
  import Appointments from "../components/Appointments";
  import AddUser from "../components/AddUser";
  export default {
    name: "Home",
    props: {
      showAddUser: Boolean,
    },
    components: {
      Appointments,
      AddUser,
    },
    data() {
      return {
        Appointment: [],
      };
    },
    methods: {
      async addUser(user) {
        const res = await fetch("api/Appointement/createAppointement", {
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
</script>
