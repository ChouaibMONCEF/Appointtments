<template>
    <div :key="User.id" v-for="User in Users">
        <User @delete-User="$emit('delete-User', User.id)" @toggle-active="$emit('toggle', User.id)"  :User="User" />
 
    </div>
</template>


<script>
import User from './User'
export default {
    name: 'Users',
    props: {
        Users: Array
    },
    components: {
        User,
    },
    emits: ['delete-User','toggle']
}
</script>