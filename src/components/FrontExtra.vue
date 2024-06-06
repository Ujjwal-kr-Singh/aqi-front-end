<template>
    <div class="container1">
      <img alt="Vue logo" src="../assets/aqi1n.jpg" class="background-img">
      <div class="container">
        <h1 class="title">Air Quality Index</h1>
        <div class="search-bar">
          <input type="text" v-model="searchQuery" placeholder="Enter your location" />
          <button @click="searchLocation">Search</button>
        </div>
        <div v-if="isLoading" class="loading">
          Loading...
        </div>
        <div v-else-if="error" class="error">
          {{ error.message }}
        </div>
        <div v-else class="data">
          <div class="location">
            <h2>{{ location }}</h2>
          </div>
  
          <div class="index">
            <h2>Air Quality Index: {{ aqi }}</h2>
            <p>Status: {{ getStatus(aqi) }}</p>
            <div class="aqi-circle" :style="{ backgroundColor: getAqiColor(aqi) }">
              {{ aqi }}
            </div>
          </div>
  
          <div class="details">
            <div v-for="(value, key) in pollutants" :key="key">
              <h3>{{ key }} : {{ value }}</h3>
            </div>
          </div>
  
          <!-- Chart visualization goes here -->
          <div class="chart">
            <h2>Air Quality Image: {{ aqi }}</h2>
            <p>Status: {{ getStatus(aqi) }}</p>
            <!-- <img alt="Vue logo" src=getImage(aqi)> -->
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  export default {
    name: 'FrontExtra',
    data() {
      return {
        searchQuery: '',
        location: '',
        aqi: null,
        pollutants: {},
        isLoading: false,
        error: null,
      };
    },
    methods: {
      searchLocation() {
        this.isLoading = true;
        this.error = null;
        const apiKey = 't+O/4XAQnZ9NUcDswHrLnw==2f5ebMbPzv0PA47r';
        const apiUrl = 'https://api.api-ninjas.com/v1/airquality';
  
        axios
          .get(apiUrl, {
            params: {
              city: this.searchQuery,
              'X-Api-Key': apiKey,
            },
          })
          .then(response => {
            console.log(response, 'res...');
            this.location = response.data.data.city;
            this.aqi = response.data.overall_aqi;
            this.pollutants = response.data;
            this.isLoading = false;
          })
          .catch(errorapi => {
            this.error = errorapi.message;
            console.log(this.error);
            this.isLoading = false;
          });
      },
      getStatus(aqi) {
        if (aqi == null) {
          return 'No Data';
        } else if (aqi <= 50) {
          return 'Good🟩';
        } else if (aqi <= 100) {
          return 'Moderate🟦';
        } else if (aqi <= 150) {
          return 'Unhealthy for Sensitive Groups🟪';
        } else if (aqi <= 200) {
          return 'Unhealthy🟧';
        } else if (aqi <= 300) {
          return 'Very Unhealthy❌';
        } else {
          return 'Hazardous💀';
        }
      },
      getAqiColor(aqi) {
        if (aqi == null) {
          return 'transparent';
        } else if (aqi <= 50) {
          return 'green';
        } else if (aqi <= 100) {
          return 'yellow';
        } else if (aqi <= 150) {
          return 'orange';
        } else if (aqi <= 200) {
          return 'red';
        } else if (aqi <= 300) {
          return 'purple';
        } else {
          return 'brown';
        }
      },
    },
  };
  </script>
  
  <style scoped>
  .container1 {
    background-image: url("@/assets/cop.avif");
    background-size: cover;
    background-repeat: no-repeat;
    min-height: 10vh;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  
  .background-img {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    opacity: 0.2; /* Adjust opacity as needed */
    z-index: -1; /* Place behind the content */
  }
  
  .container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 120vh;
  }
  
  .title {
    margin-bottom: 10px;
    margin-top: 7rem;
    margin-right: 1rem;
  }
  
  .search-bar {
    display: flex;
    margin-bottom: 20px;
  }
  
  .search-bar input {
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px 0 0 5px;
  }
  
  .search-bar button {
    padding: 20px 20px;
    background-color: #4CAF50;
    color: rgb(255, 255, 255);
    border: none;
    border-radius: 0 5px 5px 0;
    cursor: pointer;
  }
  
  .search-bar button:hover {
    background-color: #05650d;
  }
  
  .loading {
    font-size: 24px;
    font-weight: bold;
  }
  
  .error {
    color: red;
    font-weight: bold;
  }
  
  .data {
    display: flex;
    flex-direction: column;
    align-items: start;
    justify-content: center;
  }
  
  .location {
    margin-bottom: 20px;
  }
  
  .index {
    margin-bottom: 20px;
    align-items: left;
    font-size: 10px;
  }
  
  .details {
    margin-bottom: 10px;
    align-items: top;
    font-size: 15px;
  }
  
  .chart {
    width: 70%;
    height: 250px;
    border: 2px solid #27a4a7;
    align-self: flex-start;
  }
  
  .aqi-circle {
    width: 90px;
    height: 80px;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 25px;
    font-weight: bold;
    margin: 20px;
  }
  </style>