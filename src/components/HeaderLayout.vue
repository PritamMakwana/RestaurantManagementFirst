<template>
    <div class="nav">
        <router-link to="/">Home</router-link>
        <router-link to="add">Add Restaurant</router-link>
        <router-link to="update">Update Restaurant</router-link>
        <a v-on:click="logout">Logout</a>
    </div>
</template>
<script>
export default {
    name: 'HeaderLayout',
    methods: {
        logout() {
            localStorage.clear();
            this.$router.push({name:"LoginPage"})
        }
    }
}
</script>
<style>
.nav {
    background-color: #333;
    overflow: hidden;
}

.nav a {
    float: left;
    color: #f2f2f2;
    text-align: center;
    padding: 16px 14px;
    text-decoration: none;
    font-size: 14px;
    margin-right: 4px;
}

.nav a:hover {
    background-color: #ddd;
    color: #222;
}
</style>