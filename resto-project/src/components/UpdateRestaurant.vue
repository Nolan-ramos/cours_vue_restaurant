<template>
    <div class="container_update_restaurant">
        <Header/>
        <h1 class="container_update_restaurant--title">hello user, Welcome to update restaurant page</h1>
        <div class="container_update_restaurant--form form">
            <input type="text" name="name" placeholder="Enter new restaurant name" v-model="restaurant.name">
            <input type="text" name="address" placeholder="Enter new restaurant address" v-model="restaurant.address">
            <input type="text" name="contact" placeholder="Enter new restaurant contact" v-model="restaurant.contact">
            <input type="submit" v-on:click="updateRestaurant()" value="Update">
        </div>
    </div>
</template>
<script>
    import axios from 'axios'
    import Header from './Header.vue'
    export default {
        name :'UdpateRestaurant',
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
            async updateRestaurant(){
                let result = await axios.put('http://localhost:3000/restaurants/'+this.$route.params.id,{
                    name:this.restaurant.name,
                    address:this.restaurant.address,
                    contact:this.restaurant.contact
                });
                if(result.status==200){
                    this.$router.push({name:'Home'})
                }
            }
        },
        async mounted(){
            let user = localStorage.getItem('user-info');
            if(!user){
                this.$router.push({name:'Login'})
            }

            const result = await axios.get('http://localhost:3000/restaurants/'+this.$route.params.id)
            this.restaurant=result.data
        }
    }
    
</script>
<style lang="scss">
    .container_update_restaurant{
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