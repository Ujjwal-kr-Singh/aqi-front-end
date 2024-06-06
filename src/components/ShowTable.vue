<template>
  <head>
    <title>Bootstrap Example</title>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
  </head>
  <body>
    <div class="background">
      <div class="wrapper">
        <div class="container mt-5">
          <div class="table-responsive">
            <table class="table table-bordered table-striped">
              <thead class="thead-dark">
                <tr>
                  <th colspan="2" class="text-center"><u><b>Air Quality Information</b></u></th>
                </tr>
              </thead>
              <tbody v-if="apiData && Object.keys(apiData).length > 0">
                <tr>
                  <td><b>City Name</b></td>
                  <td><b>{{ apiData.cityName }}</b></td>
                </tr>
                <tr>
                  <td><b>Overall AQI</b></td>
                  <td><b>{{ apiData.overall_aqi }}</b></td>
                </tr>
                <tr v-for="item in filteredData" :key="item.key">
                  <td><b>{{ item.key }} Concentration</b></td>
                  <td><b>{{ item.value.concentration }}</b></td>
                </tr>
                <tr v-for="item in filteredData" :key="item.key + 'aqi'">
                  <td><b>{{ item.key }} AQI</b></td>
                  <td><b>{{ item.value.aqi }}</b></td>
                </tr>
                <tr>
                  <td><b>Date</b></td>
                  <td><b>{{ formattedDate }}</b></td>
                </tr>
                <tr>
                  <td><b>Time</b></td>
                  <td><b>{{ formattedTime }}</b></td>
                </tr>
              </tbody>
              <tbody v-else>
                <tr>
                  <td colspan="2" class="text-center">Loading data...</td>
                </tr>
              </tbody>
            </table>
          </div>
          <div class="text-center mt-3">
            <button class="btn btn-info" @click="goBack">Back</button>
          </div>
        </div>
      </div>
    </div>
  </body>
</template>




  <script>
import 'bootstrap/dist/css/bootstrap.min.css'
import 'bootstrap/dist/js/bootstrap.bundle.min.js'
  import axios from 'axios';
  // import router from '@/router';
  import { useRoute } from 'vue-router';

  export default {
    name: "ShowTable",
    data() {
      return {
        searchQuery:'',
        apiData: [],
        err: false,
      };
    },
    created(){
       this.getvalues();

    },
    
    computed: {
      filteredData() {
      return Object.entries(this.apiData)
        .filter(([key]) => key !=='_id' && key !=='__v' && key !== 'cityName' && key !== 'overall_aqi' && key !== 'createdAt')
        .map(([key, value]) => ({ key, value }));
    },
      formattedDate() {
        return this.apiData.createdAt.toLocaleDateString();
      },
      formattedTime() {
        return this.apiData.createdAt.toLocaleTimeString();
      },
    },
    methods: {
      goBack() {
        window.history.back();
      },
      async getvalues() {
        try{
        const route= useRoute();
        this.searchQuery = await route.params.id;
        console.log( 'Product ID:', this.searchQuery);
        let result = await axios({
                method:'get',
                url:'http://localhost:3000/get/'+this.searchQuery,
            })
            console.log(result);
            if (result.data.success== true) {
            this.apiData= await result.data.data;
            this.apiData.createdAt= new Date(this.apiData.createdAt);
            this.apiData.cityName= this.apiData.cityName.toUpperCase();
            this.err = false;
            // console.log(this.apiData.createdAt);
          }
            else {
              this.err = true;
              console.log("##error in get##");
            }
          }
        catch(e)    {  
          this.err = true;
          console.log(e.message,"error");        }
            
            
      },
    },
    
  };
  </script>
  
  <style scoped>
  .table-responsive {
    margin-top: -14px;
    box-shadow: 10px 10px 10000px 20px;
    color: rgb(0, 0, 0); 

    

  }
  .btn-info {
    margin-top: 20px;
  }
  table {
    width: 100%;
    border-collapse:separate;
  }
  
  td {
    border: 1px solid #ddd;
    padding: 7px;
  }
  
  button {
    margin-top: 5rem;
    margin-bottom: 10rem;
  }
  table {
    text-align: center;
  }
  .taable{
    color: rgb(255, 255, 255); 
    margin-top: 1.5rem;
    background-image: url('@/assets/bg/bg6.jpg');
    background-repeat: no-repeat;
    background-size :  200%;  
    padding-bottom: 4rem;
    margin-bottom: 4rem;
    margin-left: 13%;
    max-width: 70%;
    box-shadow: 10px 10px 100px 20px;

  }
  .cutsom-btn{ 
    margin-bottom: 5rem;
  }
  body{
    background-color: black;
    padding: auto;
  }
  .wrapper {
    padding: 20px; /* Adjust as needed */
}
  .background{
    background-image:url("@/assets/new3.jpg");
    background-size: cover ;
    margin: auto;
    margin-top: -0px;
    padding: auto;
  background-repeat: no-repeat; /* Do not repeat the image */
  scroll-behavior:smooth;

  }
  </style>
  