<template>
    <footer>
        <router-link to="/about">About</router-link> &nbsp;
        <!-- <router-link v-if="localstorage.getItem`id` @click='logout()' to="/Logout">Logout</router-link> -->
        <p>YouCode &copy; 2021</p>
    </footer>
</template>


<style scoped>
a {
  color: #333;
}
footer {
  margin-top: 30px;
  text-align: center;
}
</style>