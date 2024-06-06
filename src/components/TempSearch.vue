<template>
    <div id="app">
      <div class="container">
        <h1>Temperature Checker</h1>
        <div class="search-bar">
          <input
            v-model="newCity"
            type="text"
            placeholder="Enter city name"
            @keydown.enter="searchCity"
          />
          <button @click="searchCity">Search</button>
        </div>
        <div class="card" v-if="cityData">
          <div class="card-header">
            <h3>{{ cityData.city }}</h3>
            <p>{{ cityData.date }}</p>
          </div>
          <div class="card-body">
            <div class="temp-container">
              <img :src="getTempIcon(cityData.temp)" alt="Temperature Icon" class="temp-icon" />
              <span class="temp">{{ cityData.temp }}&deg;</span>
              <span class="temp-unit">{{ cityData.unit }}</span>
            </div>
            <p class="description">{{ cityData.description }}</p>
          </div>
          <div class="card-footer">
            <button @click="toggleUnit">
              <span v-if="cityData.unit === 'C'">Switch to F</span>
              <span v-if="cityData.unit === 'F'">Switch to C</span>
            </button>
          </div>
        </div>
        <div v-else>
          <p>Loading data...</p>
        </div>
      </div>
      <div class="foot"></div>
    </div>
  </template>
  
  <script>
  import axios from 'axios'; // Assuming you have Axios installed
  
  const apiKey = "7aed4770a81d4893ed2f5bffc1b346a2";
  const apiUrl = "https://api.openweathermap.org/data/2.5/weather?units=metric&q=";
  
  export default {
    name: 'TempView',
    data() {
      return {
        cityData: null, // To store the data of the searched city
        newCity: '' // To store the new city input by the user
      };
    },
    methods: {
      async searchCity() {
        if (!this.newCity) return;
  
        try {
          const response = await axios.get(`${apiUrl}${this.newCity}&appid=${apiKey}`);
          this.cityData = {
            id: response.data.id,
            city: response.data.name,
            temp: response.data.main.temp,
            date: new Date().toLocaleDateString(),
            description: response.data.weather[0].description,
            unit: 'C', // Default unit to Celsius
          };
          this.newCity = ''; // Clear the input field after adding the new city
        } catch (error) {
          console.error('Error fetching data for the new city:', error);
        }
      },
      getTempIcon(temp) {
        // Implement logic to choose an appropriate temperature icon based on temperature value
        if (temp > 25) {
          return require('@/assets/temp/hot.jpeg'); // Replace with your icon path
        } else if (temp < 10) {
          return require('@/assets/temp/cold.jpeg'); // Replace with your icon path
        } else {
          return require('@/assets/temp/neutral.jpeg'); // Replace with your icon path
        }
      },
      toggleUnit() {
        try {
          this.cityData.unit = this.cityData.unit === 'C' ? 'F' : 'C';
          // Convert temperature value to the new unit if necessary
          if (this.cityData.unit === 'F') {
            this.cityData.temp = Math.round(this.cityData.temp * 9 / 5 + 32);
          } else {
            this.cityData.temp = Math.round((this.cityData.temp - 32) * 5 / 9);
          }
        } catch (error) {
          console.error('Error toggling unit:', error);
        }
      },
    },
  };
  </script>
  
  <style scoped>
  .container {
    max-width: 800px;
    margin: 0 auto;
    padding: 20px;
    margin-top: -1%;
  }
  
  .search-bar {
    display: flex;
    justify-content: center;
    margin-bottom: 20px;
  }
  
  .search-bar input {
    padding: 10px;
    font-size: 1em;
    border: 1px solid #ccc;
    border-radius: 5px;
    margin-right: 10px;
  }
  
  .search-bar button {
    background-color: #007bff;
    color: white;
    border: none;
    padding: 10px 20px;
    border-radius: 5px;
    cursor: pointer;
  }
  
  .search-bar button:hover {
    background-color: #0056b3;
  }
  
  .card {
    background-color: #ffffff;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    border-radius: 5px;
    padding: 20px;
    text-align: center;
    margin-bottom: 20px;
  }
  
  .card-header {
    margin-bottom: 10px;
  }
  
  .temp-container {
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 10px;
  }
  
  .temp {
    font-size: 2em;
    margin-left: 10px;
  }
  
  .temp-unit {
    font-size: 1.2em;
    margin-left: 5px;
  }
  
  .description {
    margin: 10px 0;
  }
  
  .card-footer {
    margin-top: 10px;
  }
  
  button {
    background-color: #007bff;
    color: white;
    border: none;
    padding: 10px 20px;
    border-radius: 5px;
    cursor: pointer;
  }
  
  button:hover {
    background-color: #0056b3;
  }
  
  /* Define the style for the temperature icon */
  .temp-icon {
    width: 50px;
    height: 50px;
    margin-right: 10px;
  }
  
  h1 {
    color: #ffffff;
  }
  
  .foot {
    margin: 5%;
  }
  </style>
  