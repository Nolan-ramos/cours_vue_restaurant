<template>
    <div class="container_header">
        <nav>
            <router-link to="/">Home</router-link>
            <router-link to="/add-restaurant">Add Resutaurant</router-link>
            <a href="#" v-on:click="logout">Logout</a>
        </nav>
    </div>
</template>
<script>
    export default {
        name :'Header',
        methods:{
            logout(){
                localStorage.clear();
                this.$router.push({name:'Login'})
            }
        }
    }
</script>
<style lang="scss">
    .container_header{
        nav{
            width: 100%;
            position: absolute;
            top:0;
            left:0;
            border-bottom: solid 1px black ;
            padding:20px;
            a{
                margin-right: 20px;
                &:last-child{
                    margin-left: 0;
                }
                &:hover{
                    color: #8CC63F;
                }
            }
        }
    }
</style>