<template>
    <div class="container_home">
        <Header/>
        <h1 class="container_home--title">hello {{ user_info.name }}, Welcome to home page</h1>
        <div class="container_home--all_restaurants">
            <div class="container_home--all_restaurants--restaurant" v-for="item in restaurants" :key=item.id>
                <span>{{ item.name }}</span>
                <span>{{ item.contact }}</span>
                <span>{{ item.address }}</span>
                <span><router-link :to="'/update-restaurant/'+item.id">Update</router-link></span>
                <button v-on:click="deleteRestaurant(item.id)">Delete</button>
            </div>
        </div>
    </div>
</template>
<script>
    import axios from 'axios'
    import Header from './Header.vue'
    export default {
        name :'Home',
        components:{
            Header
        },
        data(){
            return{
                user_info:'',
                restaurants:[],
            }
        },
        methods:{
            async deleteRestaurant(id){
                let result = await axios.delete('http://localhost:3000/restaurants/'+id);
                if(result.status == 200){
                    this.loadData()
                }
            },
            async loadData(){
                let user = localStorage.getItem('user-info');
                this.user_info = JSON.parse(user)
                if(!user){
                    this.$router.push({name:'Login'})
                }

                let result = await axios.get('http://localhost:3000/restaurants');
                    this.restaurants = result.data;
                }
        },
        async mounted(){
            this.loadData()
        }
    }
    
</script>
<style lang="scss">
    .container_home{
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
        height:100vh;
        &--title{
            margin-bottom: 20px;
        }
        &--all_restaurants{
            border:solid 1px black;
            &--restaurant{
                border-bottom: solid 1px black;
                display: flex;
                &:last-child{
                    border-bottom-width: 0;
                }
                span{
                    padding: 10px;
                    display: block;
                }
            }
        }
    }
</style>