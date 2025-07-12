<template>
      <HeaderLayout />
    <h1>Hello,welcome On UpdatePage page</h1>
</template>
<script>
import HeaderLayout from './HeaderLayout.vue'
export default {
    name: "UpdatePage",
    components: {
        HeaderLayout
    },
    mounted() {
        let user = localStorage.getItem('user-info');
        if (!user) {
            this.$router.push({ name: "SignUp" });
        }
    }
};
</script>