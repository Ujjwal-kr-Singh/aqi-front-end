<template>
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Document</title>
    </head>
    <body>
      <div id="container">

        <nav class="navbar">
          <!-- <div class="navbar-top">
          <button @click="toggleSidebar" class="sidebar-toggle">
            ☰
          </button>
        </div> -->
        <SideBar />
        <div class="date">
          <span style="">{{ moment(new Date()).format('DD-MM-YYYY') }}</span>
        </div>
        <div class="navbar-right">
          <button @click="login" class="nav-button">Login</button>
          <button @click="signup" class="nav-button ">Sign Up</button>
        </div>
      </nav>
      
    </div>
</body>
</html>
  </template>
  <script>
  import router from '@/router';
   var moment = require('moment');
  import SideBar from './SideBar.vue';
  export default {
    name: 'HeaderFile',
    components:{
      SideBar,
    },
    methods: {
      toggleSidebar() {
        // Implement your sidebar toggle logic here
        console.log('Sidebar toggled');
      },
      login() {
        // Implement your login logic here
        console.log('Login clicked');
        router.push('/login');
      },
      signup() {
        // Implement your sign-up logic here
        console.log('Sign Up clicked');
        router.push('/Signup');
      }
    },
    data() {
      return {
         moment,
        // Implement your data here
      }
    }
  }
  </script>
  
  <style scoped>
  #container {
    box-shadow: 0 0 20px 10px rgba(0, 0, 0, 0.5);
}

  .navbar {
    justify-content: space-between;
    align-items: center;
    background-color: rgb(0, 0, 0);
    padding: 10px 20px;
    color: white; 
    margin-top: -60px;
    padding:1.3%;
    border: auto;
    box-shadow: 100%;    
  }
  
  SideBar{
    background-color: #282121;
    
  }
  .navbar-right .nav-button {
    background-color: #42b983;
    border: none;
    color: white;
    padding: 10px 20px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    margin: 4px 2px;
    cursor: pointer;
    border-radius: 12px;
    transition: background-color 0.3s ease;
    margin-left: 10px;
  }
  
  .navbar-right .nav-button:hover {
    background-color: #05650d;
  }
  .date{
    color: rgb(0, 64, 255);
    font-size: 20px;
    box-shadow: #282121;
    text-align: center;
    margin-left: 7%;
  }
  </style>
  