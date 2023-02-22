<template>
    <div class="container_add_restaurant">
        <Header/>
        <h1 class="container_add_restaurant--title">hello user, Welcome to add restaurant page</h1>
        <div class="container_add_restaurant--form form">
            <input type="text" name="name" placeholder="Enter restaurant name" v-model="restaurant.name">
            <input type="text" name="address" placeholder="Enter restaurant address" v-model="restaurant.address">
            <input type="text" name="contact" placeholder="Enter restaurant contact" v-model="restaurant.contact">
            <input type="submit" v-on:click="addRestaurant()" value="Add">
        </div>
    </div>
</template>
<script>
    import axios from 'axios'
    import Header from './Header.vue'
    export default {
        name :'AddRestaurant',
        components:{
            Header
        },
        data(){
            return{
                restaurant:{
                    name:'',
                    address:'',
                    contact:''
                }
            }
        },
        methods:{
            async addRestaurant(){
                let result = await axios.post('http://localhost:3000/restaurants',{
                    name:this.restaurant.name,
                    address:this.restaurant.address,
                    contact:this.restaurant.contact
                });
                if(result.status==201){
                    this.$router.push({name:'Home'})
                }
            }
        },
        mounted(){
            let user = localStorage.getItem('user-info');
            if(!user){
                this.$router.push({name:'Login'})
            }
        }
    }
    
</script>
<style lang="scss">
    .container_add_restaurant{
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
        height:100vh;
        &--title{
            margin-bottom: -10px;
        }
    }
</style>