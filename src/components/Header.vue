<template>
    <header>
        
            
        <h3>Ref:{{title}}</h3>
        <router-link to="/Login">Login</router-link> &nbsp;
        <router-link to="/">Appointements</router-link> &nbsp;
        <router-link to="/Register">Register</router-link>
        <Button v-show="homePage" @btn-click="$emit('toggle-add-User')" 
        :text="showAddUser ? 'Close' : 'Add' " 
        :color="showAddUser ? 'red' : 'green' " 
         />
        
    </header>
</template>

<script>

import Button from "./Button"

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
    header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 20px;

    }
</style>