<template>
  <div v-show="showAddUser">
    <AddUser @add-User="addUser" />
  </div>
  <!-- CUSTOM EVENT LISTENER -->
  <Users @toggle="toggleActive" @delete-User="deleteUser" :Users="Users" />
</template>

<script>
  import Users from "../components/Users";
  import AddUser from "../components/AddUser";
  export default {
    name: "Home",
    props: {
        showAddUser: Boolean,
    },
    components: {
      Users,
      AddUser,
    },
    data() {
      return {
        Users: [],
      };
    },
    methods: {
      async addUser(user) {
        const res = await fetch("api/Users", {
          method: "POST",
          headers: {
            "Content-type": "application/json",
          },
          body: JSON.stringify(user),
        });

        const data = await res.json();

        this.Users = [...this.Users, data];
      },
      async deleteUser(id) {
        if (confirm("are you sure?")) {
          const res = await fetch(`api/Users/${id}`, {
            method: "DELETE",
          });

          res.status === 200
            ? (this.Users = this.Users.filter((User) => User.id !== id))
            : alert("error deleting user");
        }
      },
      async toggleActive(id) {
        const usertoggle = await this.fetchUser(id);
        const updateuser = { ...usertoggle, active: !usertoggle.active };

        const res = await fetch(`api/Users/${id}`, {
          method: "PUT",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify(updateuser),
        });

        const data = await res.json();

        this.Users = this.Users.map((User) =>
          User.id === id ? { ...User, active: data.active } : User
        );
      },
      async fetchUsers() {
        const res = await fetch("api/Users");

        const data = await res.json();
        return data;
        
      },
      async fetchUser(id) {
        const res = await fetch(`api/Users/${id}`);

        const data = await res.json();

        return data;
      },
    },
    
    async created() {
     
      this.Users = await this.fetchUsers();
    },
  };
</script>
