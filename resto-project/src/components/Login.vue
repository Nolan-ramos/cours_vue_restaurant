<template>
    <div class="container_login">
        <img class="container_login--logo" alt="Vue logo" src="../assets/logo.png">
        <h1 class="container_login--title">Login</h1>
        <div class="container_login--form form">
            <input type="mail" v-model="email" placeholder="Enter Email">
            <input type="password" v-model="password" placeholder="Enter Password">
            <input v-on:click="login()" type="submit" value="Login">
            <router-link to="/sign-up">Sign up</router-link>
        </div>
    </div>
</template>
<script>
    import axios from 'axios'
    export default {
        name :'Login',
        data(){
            return{
                email:'',
                password:''
            }
        },
        methods:{
            async login(){
                let result = await axios.get(
                    `http://localhost:3000/users?email=${this.email}&password=${this.password}`
                )
                if(result.status==200 && result.data.length > 0){
                    localStorage.setItem("user-info",JSON.stringify(result.data[0]))
                    this.$router.push({name:'Home'})
                }
            }
        },
        mounted(){
            let user = localStorage.getItem('user-info');
            if(user){
                this.$router.push({name:'Home'})
            }
        }
    }
    
</script>
<style lang="scss">

</style>