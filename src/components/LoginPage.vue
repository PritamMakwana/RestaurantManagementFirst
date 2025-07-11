<template>
    <img src="../assets/restaurant-logo.jpg" alt="Logo" class="logo" />
    <h1>Login</h1>
    <div class="login">
        <input type="email" v-model="email" placeholder="Enter email" />
        <input type="password" v-model="password" placeholder="Enter Password" />
        <button v-on:click="login">Login</button>
        <p>
            <router-link to="/sign-up">Sign Up</router-link>
        </p>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    name: "LoginPage",
    data() {
        return {
            email: '',
            password: '',
        }
    },
    methods: {
        async login() {
            let result = await axios.get(
                `http://localhost:3000/user?email=${this.email}&password=${this.password}`
            )

            console.log("Result from server", result);
            if (result.status === 200 && result.data.length > 0) {
                // alert("User login successfully");
                localStorage.setItem("user-info", JSON.stringify(result.data[0]));
                this.$router.push({ name: 'HomePage' });
            } else {
                alert("Input Invalid  in login");
            }
        }
    },
    mounted() {
        let user = localStorage.getItem('user-info');
        if (user) {
            this.$router.push({ name: "HomePage" });
        }
    }
}
</script>
