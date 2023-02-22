<template>
    <div class="container_sign_up">
        <img class="container_sign_up--logo" alt="Vue logo" src="../assets/logo.png">
        <h1 class="container_sign_up--title">Sign Up</h1>
        <div class="container_sign_up--form form">
            <input type="text" v-model="name" placeholder="Enter Name">
            <input type="mail" v-model="email" placeholder="Enter Email">
            <input type="password" v-model="password" placeholder="Enter Password">
            <input v-on:click="signUp()" type="submit" value="Sign up">
            <router-link to="/login">Login</router-link>
        </div>
    </div>
</template>
<script>
    import axios from 'axios'
    export default {
        name :'SignUp',
        data(){
            return{
                name:'',
                email:'',
                password:'',
            }
        },
        methods:{
            async signUp(){
                let result = await axios.post("http://localhost:3000/users",{
                    email:this.email,
                    password:this.password,
                    name:this.name
                });
                console.log(result);
                if(result.status==201){
                    localStorage.setItem("user-info",JSON.stringify(result.data))
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