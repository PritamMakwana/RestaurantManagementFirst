<template>

    <img src="../assets/restaurant-logo.jpg" alt="Logo" class="logo" />
    <h1>Sign Up</h1>
    <div class="register">
        <input type="text" placeholder="Enter name" />
        <input type="text" placeholder="Enter email" />
        <input type="password" placeholder="Enter Password" />
        <button>Sign Up</button>
    </div>
</template>
<script>
export default {
    name: "SignUp",

}
</script>
<style>
.logo {
    width: 100px;
}

.register input{
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