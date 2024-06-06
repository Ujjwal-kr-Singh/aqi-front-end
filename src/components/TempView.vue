<template>
    <div id="app">
      <div class="container">
        <h1>Temperature across the world</h1>
        <div class="cards" v-if="data.length > 0">
          <div class="card" v-for="(item, index) in data" :key="item.id">
            <div class="card-header">
              <h3>{{ item.city }}</h3>
              <p>{{ item.date }}</p>
            </div>
            <div class="card-body">
              <div class="temp-container">
                <img :src="getTempIcon(item.temp)" alt="Temperature Icon" class="temp-icon" />
                <span class="temp">{{ item.temp }}&deg;</span>
                <span class="temp-unit">{{ units[index] }}</span>
              </div>
              <p class="description">{{ item.description }}</p>
            </div>
            <div class="card-footer">
              <button @click="toggleUnit(index)">
                <span v-if="units[index] === 'C'">Switch to F</span>
                <span v-if="units[index] === 'F'">Switch to C</span>
              </button>
            </div>
          </div>
        </div>
        <div v-else>
          <p>Loading data...</p>
        </div>
      </div>
    </div>
    <div class="foot"></div>
  </template>

  <script>
import axios from 'axios'; // Assuming you have Axios installed

const apiKey = "7aed4770a81d4893ed2f5bffc1b346a2";
const apiUrl = "https://api.openweathermap.org/data/2.5/weather?units=metric&q=";

export default {
  name: 'TempView',
  data() {
    return {
      data: [],
      units: [], // Array to store temperature units (C or F)
    };
  },
  mounted() {
    this.fetchData();
  },
  methods: {
    async fetchData() {
      const cities = ["New York", "London", "Tokyo", "Delhi"]; // Add more cities as needed
      const weatherDataPromises = cities.map(city =>
        axios.get(`${apiUrl}${city}&appid=${apiKey}`)
      );

      try {
        const responses = await Promise.all(weatherDataPromises);
        this.data = responses.map(response => ({
          id: response.data.id,
          city: response.data.name,
          temp: response.data.main.temp,
          date: new Date().toLocaleDateString(),
          description: response.data.weather[0].description,
        }));
        this.units.length = this.data.length; // Initialize units array
        this.units.fill('C'); // Set default unit to Celsius
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    },
    getTempIcon(temp) {
      // Implement logic to choose an appropriate temperature icon based on temperature value
      // This could involve using a CSS class or dynamically setting an image source
      if (temp > 25) {
        return require('@/assets/temp/hot.jpeg'); // Replace with your icon path
      } else if (temp < 10) {
        return require('@/assets/temp/cold.jpeg'); // Replace with your icon path
      } else {
        return require('@/assets/temp/neutral.jpeg'); // Replace with your icon path
      }
    },
    toggleUnit(index) {
      try {
        this.units[index] = this.units[index] === 'C' ? 'F' : 'C';
        // Convert temperature value to the new unit if necessary
        if (this.units[index] === 'F') {
          this.data[index].temp = Math.round(this.data[index].temp * 9 / 5 + 32);
        } else {
          this.data[index].temp = Math.round((this.data[index].temp - 32) * 5 / 9);
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

.cards {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  gap: 20px;
}

.card {
  background-color: #ffffff;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  border-radius: 5px;
  padding: 20px;
  text-align: center;
  flex: 1 1 calc(50% - 20px);
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
  h1{
    color: #007bff;
  }
  .foot{
    margin: 05%;
  }
</style>
