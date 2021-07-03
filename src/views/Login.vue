<template>
  <div class="form">
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
  </div>
</template>

<script>

import Button from "../components/Button"

export default { 
    name: 'Header',
    props: {
        title: String,
        showAddUser: Boolean
    },
    components: {
        
        Button,
    },
    computed: {
        homePage() {
            if(this.$route.path === '/') {
                return true
            } else {
                return false
            }
        }
    }
}
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
