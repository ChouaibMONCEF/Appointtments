<template>
    <div class="form">
    <form class="register" action="">
      <h1>Welcome back</h1>
      <div class="fclass">
        <label for="FirstName">First Name</label> <br> <br>
        <input
          type="text"
          name="FirstName"
          id="FirstName"
          placeholder=" Chouaib "
        />
      </div>
      <div class="fclass">
        <label for="LastName">Last Name</label> <br> <br>
        <input
          type="text"
          name="LastName"
          id="FirstName"
          placeholder=" Moncef "
        />
      </div>
      <div class="fclass">
        <label for="email">Email</label> <br> <br>
        <input
          type="text"
          name="email"
          id="FirstName"
          placeholder=" Choaibmoncef1@gmail.com "
        />
      </div>
      <br>
      <Button  />
    </form>
  </div>
</template>

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