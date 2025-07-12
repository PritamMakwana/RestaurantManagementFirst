<template>
    <HeaderLayout />
    <h1>Hello,{{ name }} On HomePage page</h1>
    <table border="1">
        <tr>
            <th>Id</th>
            <th>Name</th>
            <th>Aaddress</th>
            <th>Contact</th>
            <th>Action</th>
        </tr>
        <tr v-for="item in restaurants" :key="item.id">
            <td>{{ item.id }}</td>
            <td>{{ item.name }}</td>
            <td>{{ item.address }}</td>
            <td>{{ item.contact }}</td>
            <td><router-link :to="'/update/' + item.id">Update</router-link>
                <button v-on:click="deleteRestarent(item.id)">delete</button>
            </td>
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
    methods: {
        async deleteRestarent(id) {
            console.log('delete' + id);
            let result = await axios.delete("http://localhost:3000/restaurant/" + id);
            if (result.status == 200) {
                console.log('delete');
                this.loadData();
            }
        },
        async loadData() {
            let user = localStorage.getItem('user-info');
            this.name = JSON.parse(user).name
            if (!user) {
                this.$router.push({ name: "SignUp" });
            }
            let result = await axios.get("http://localhost:3000/restaurant");
            this.restaurants = result.data;
        }
    },
    async mounted() {
        this.loadData();
    }
};
</script>
<style>
td {
    width: 160px;
    height: 40px;
}
</style>