<template>

    <img src="../assets/restaurant-logo.jpg" alt="Logo" class="logo" />
    <h1>Sign Up</h1>
    <div class="register">
        <input type="text" v-model="name" placeholder="Enter name" />
        <input type="text" v-model="email" placeholder="Enter email" />
        <input type="password" v-model="password" placeholder="Enter Password" />
        <button v-on:click="signUp">Sign Up</button>
    </div>
</template>
<script>
import axios from 'axios';
export default {
    name: "SignUp",
    data() {
        return {
            name: '',
            email: '',
            password: '',
        }
    },
    methods: {
        async signUp() {
            console.log("Sign Up clicked", this.name, this.email, this.password);
            let result = await axios.post("http://localhost:3000/user", {
                name: this.name,
                email: this.email,
                password: this.password
            });
            console.log("Result from server", result);
            if (result.status === 201) {
                // alert("User registered successfully");
                localStorage.setItem("user-info", JSON.stringify(result.data));
                this.$router.push({ name: 'HomePage' });
            } else {
                alert("Error in registration");
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
<style>
.logo {
    width: 100px;
}

.register input {
    width: 300px;
    height: 40px;
    padding-left: 20px;
    display: block;
    margin-bottom: 30px;
    margin-left: auto;
    margin-right: auto;
    border: 1px solid yellow;
}

.register button {
    width: 320px;
    height: 40px;
    background-color: yellow;
    color: black;
    font-weight: bold;
    border: none;
    cursor: pointer;
}
</style>