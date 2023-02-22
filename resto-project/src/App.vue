<template>
    <router-view></router-view>
</template>

<script>
export default {
  name: 'App',
}
</script>

<style lang="scss">
@import url('style/reseet.css');
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');
#app {
  font-family: 'Roboto', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;  
}
.container_sign_up,
.container_login{
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  height:100vh;
  &--logo{
      width:200px;
  }
  &--title{
      margin-top: 30px;
      font-size: 48px;
  }
  &--form{
      
  }
}
.form{
    margin-top: 30px;
    display: flex;
    flex-direction: column;
    input{
        margin-bottom: 20px;
        padding:15px;
        width: 300px;
        border:solid 1px #F7941E;
        border-radius: 6px;
        &:last-child{
            margin-bottom: 0;
        }
    }
    input[type="submit"]{
        padding:15px 20px;
        background: #8CC63F;
        border:none;
        color:white;
        border-radius: 6px;
        &:hover{
            opacity:0.8;
        }
    }
    a{
        padding:15px 20px;
        background: #8CC63F;
        border:none;
        color:white;
        text-align: center;
        border-radius: 6px;
        &:hover{
            opacity:0.8;
        }
    }
}
</style>
