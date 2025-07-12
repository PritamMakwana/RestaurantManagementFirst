<template>
    <HeaderLayout />
    <h1>Hello,{{ name }} On HomePage page</h1>
    <table border="1">
        <tr>
            <th>Id</th>
            <th>Name</th>
            <th>Aaddress</th>
            <th>Contact</th>
        </tr>
        <tr v-for="item in restaurants" :key="item.id">
            <td>{{ item.id }}</td>
            <td>{{ item.name }}</td>
            <td>{{ item.address }}</td>
            <td>{{ item.contact }}</td>
        </tr>
    </table>
</template>
<script>
import axios from 'axios';
import HeaderLayout from './HeaderLayout.vue'
export default {
    name: "HomePage",
    data() {
        return {
            name: "",
            restaurants: [],
        }
    },
    components: {
        HeaderLayout
    },
    async mounted() {
        let user = localStorage.getItem('user-info');
        this.name = JSON.parse(user).name
        if (!user) {
            this.$router.push({ name: "SignUp" });
        }
        let result = await axios.get("http://localhost:3000/restaurant");
        this.restaurants = result.data;
    }
};
</script>
<style>
td {
    width: 160px;
    height: 40px;
}
</style>