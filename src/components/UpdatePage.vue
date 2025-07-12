<template>
    <HeaderLayout />
    <h1>Hello,welcome On UpdatePage page</h1>
    <form class="add">
        <input type="text" placeholder="Enter Name" v-model="restaurent.name" name="name" />
        <input type="text" placeholder="Enter Address" v-model="restaurent.address" name="address" />
        <input type="text" placeholder="Enter Contact" v-model="restaurent.contact" name="contact" />
        <button type="button" v-on:click="updateRestaurent">Update Restaurent</button>
    </form>
</template>
<script>
import axios from 'axios';
import HeaderLayout from './HeaderLayout.vue'
export default {
    name: "UpdatePage",
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
        async updateRestaurent() {
            try {
                console.log("Trying to update ID:", this.$route.params.id);
                const result = await axios.put("http://localhost:3000/restaurant/" + this.$route.params.id, {
                    name: this.restaurent.name,
                    address: this.restaurent.address,
                    contact: this.restaurent.contact
                });

                if (result.status == 200) {
                    this.$router.push({ name: 'HomePage' });
                }
            } catch (error) {
                console.error("Update failed:", error);
                alert("Update failed. Please check if the ID exists and server is running.");
            }
        }
    },
    async mounted() {

        let user = localStorage.getItem('user-info');
        if (!user) {
            this.$router.push({ name: "SignUp" });
        }

        const result = await axios.get('http://localhost:3000/restaurant?id=' + this.$route.params.id);

        this.restaurent = result.data[0];
    }
};
</script>