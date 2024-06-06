<template>
    <div class="container">
      <header class="header">
        <h1>Welcome to AQI Tracker</h1>
      </header>
  
      <main class="main">
        <!-- <div class="hero">
          <p>Track air quality, stay informed, and breathe easy.</p>
          <a href="/login" class="button primary">Login</a>
          <a href="/signup" class="button secondary">Sign Up</a>
        </div> -->
  
        <div class="search-section">
          <h2>Find Air Quality Data</h2>
          <form @submit.prevent="search">
            <input type="text" placeholder="Enter city " v-model="searchQuery" class="search-input"><br>
            <div  class="errors" v-if = "err"><p>! Could not find data...</p></div>
            <button type="submit" class="button primary">Search</button>
          </form>
        </div>
      </main>
  
      
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  import router from '@/router';
  export default {
    name: 'HomePage2',
    data() {
      return {
        searchQuery: '',
      err: false,
      };
    },
    methods: {
      async search() {
        try{
        console.log('Search:', this.searchQuery);
        let result = await axios({
                method:'post',
                url:'http://localhost:3000/airquality?city='+this.searchQuery,
                data:{ cityName: this.searchQuery },
              });
              console.log("result", result);
              this.err= false;
              console.log("city;ssss id  ",result.data.id);
            if (result.data.success) {
                router.push({ path:"/showtable/"+  result.data.id }); 
              }
              else {
                console.log("error");
                this.err= true;
              }
            }catch(e){
              this.err= true;
              console.log(e.message)}    
    },
  },
}
  </script>
  
  <style scoped>
  .container {
    display: flex;
    flex-direction: column;
    min-height: 100vh;
    font-family: 'Arial', sans-serif;
    background-color: transparent ;
    color: #333;
  background-image: url('@/assets/bg/1591945.jpg');
  background-size: cover;

  }
  
  .header {
    background-color: #333;
    color: #fff;
    padding: 20px 0px 13px 0px;
    text-align: center;
    width: 101.8%;
    margin-left: -0.7rem ;
    margin-right: 1rem ;

  }
  
  .main {
    padding: 20px;
    flex-grow: 1;
  }
  
  .hero {
    text-align: center;
    margin-bottom: 30px;
  }
  
  .hero p {
    font-size: 1.2em;
    margin-bottom: 20px;
  }
  
  .search-section {
    margin-bottom: 30px;
  }
  
  .search-input {
    margin-top: 1rem;
    padding: 10px;
    border: 1px solid #fffdfd;
    border-radius: 5px;
    width: 070%;
    box-sizing: border-box;
  }
  
  .button {
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    margin: 0 10px;
    text-decoration: none;
    font-weight: bold;
    cursor: pointer;
  }
  
  .button.primary {
    margin-top: 2rem;
    background-color: #4CAF50; /* Green */
    color: #fff;
  }
  
  .button.secondary {
    background-color: #f44336; /* Red */
    color: #fff;
  }
  
  .footer {
    background-color: #333;
    color: #fff;
    padding: 20px;
    text-align: center;
  }
  h2{
    color: #ffffff;
  }
  .errors {
    color: #ffffff;
  }
  
  </style>