<template>
    <HeaderLayout />
    <h1>Hello,welcome On AddPage page</h1>
    <form class="add">
        <input type="text" placeholder="Enter Name" v-model="restaurent.name" name="name" />
        <input type="text" placeholder="Enter Address" v-model="restaurent.address" name="address" />
        <input type="text" placeholder="Enter Contact" v-model="restaurent.contact" name="contact" />
        <button type="button" v-on:click="addRestaurent">Add New Restaurent</button>
    </form>
</template>
<script>
import axios from 'axios';
import HeaderLayout from './HeaderLayout.vue'
export default {
    name: "AddPage",
    components: {
        HeaderLayout
    },
    data() {
        return {
            restaurent: {
                name: '',
                address: '',
                contact: ''
            }

        }
    },
    methods: {
        async addRestaurent() {
            const result = await axios.post("http://localhost:3000/restaurant", {
                name: this.restaurent.name,
                address: this.restaurent.address,
                contact: this.restaurent.contact,
            });

            if (result.status == 201) {
                this.$router.push({ name: 'HomePage' });
            }
            console.warn("result", result);
        }
    },
    mounted() {
        let user = localStorage.getItem('user-info');
        if (!user) {
            this.$router.push({ name: "SignUp" });
        }
    }
};
</script>