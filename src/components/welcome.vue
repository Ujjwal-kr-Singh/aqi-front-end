<template>
  <div class="welcome-container">
    <div class="left-cards" v-if="data.length > 0">
      <div class="card" v-for="(item, index) in data.slice(0, 2)" :key="item.id">
        <div class="card-header">
          <h3>{{ item.city }}</h3>
          <p>{{ item.date }}</p>
        </div>
        <div class="card-body">
          <div class="temp-container">
            <img :src="getTempIcon(item.temp)" alt="Temperature Icon" class="temp-icon" />
            <span class="temp">{{ item.temp }}°</span>
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
    <div class="welcome-card">
      <h1>Welcome to AQI Tracker</h1>
      <p>Monitor the air quality in your city and stay informed about the latest AQI levels.</p>
      <div class="button-group">
        <button @click="navigateToFeatures">Explore Features</button>
        <button @click="navigateToAQI">View AQI</button>
      </div>
      <p class="about-link">
        <router-link to="/about">Learn more about us</router-link>
      </p>
    </div>
    <div class="right-cards" v-if="data.length > 2">
      <div class="card" v-for="(item, index) in data.slice(2, 4)" :key="item.id">
        <div class="card-header">
          <h3>{{ item.city }}</h3>
          <p>{{ item.date }}</p>
        </div>
        <div class="card-body">
          <div class="temp-container">
            <img :src="getTempIcon(item.temp)" alt="Temperature Icon" class="temp-icon" />
            <span class="temp">{{ item.temp }}°</span>
            <span class="temp-unit">{{ units[index + 2] }}</span>
          </div>
          <p class="description">{{ item.description }}</p>
        </div>
        <div class="card-footer">
          <button @click="toggleUnit(index + 2)">
            <span v-if="units[index + 2] === 'C'">Switch to F</span>
            <span v-if="units[index + 2] === 'F'">Switch to C</span>
          </button>
        </div>
      </div>
    </div>
  </div>
  <div class="foot"></div>
</template>


<script>
import router from '@/router';
import axios from 'axios'; // Assuming you have Axios installed

const apiKey = "7aed4770a81d4893ed2f5bffc1b346a2";
const apiUrl = "https://api.openweathermap.org/data/2.5/weather?units=metric&q=";

export default {
  name: 'WelcomePage',
  methods: {
    navigateToFeatures() {
      this.$router.push('/front3');
    },
    navigateToAQI() {
      router.push('/HomePage2');
    },
    async fetchData() {
      const cities = ["New York", "London", "Tokyo", "Delhi"];
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
        this.units.length = this.data.length;
        this.units.fill('C');
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    },
    getTempIcon(temp) {
      if (temp > 25) {
        return require('@/assets/temp/hot.jpeg');
      } else if (temp < 10) {
        return require('@/assets/temp/cold.jpeg');
      } else {
        return require('@/assets/temp/neutral.jpeg');
      }
    },
    toggleUnit(index) {
      try {
        this.units[index] = this.units[index] === 'C' ? 'F' : 'C';
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
  data() {
    return {
      data: [],
      units: [],
    };
  },
  mounted() {
    this.fetchData();
  },
};
</script>


<style scoped>
.welcome-container {
  display: flex;
  justify-content: center; /* Center the welcome card */
  align-items: center;
  height: 100vh;
  position: relative; /* Needed for absolute positioning of child elements */
  padding: 0 20px;
  max-width: 1000px;
  margin: 0 auto;
}

.welcome-card {
  background: rgba(255, 255, 255, 0.9);
  padding: 2rem;
  border-radius: 10px;
  box-shadow: 20px 10px 20px 10px rgba(0, 0, 0, 0.1);
  text-align: center;
  max-width: 600px;
  width: 100%;
  margin: auto;
  z-index: 1; /* Ensure it stays on top of the other elements */
}

.welcome-card h1 {
  margin-bottom: 1rem;
  font-size: 2.5rem;
  color: #333;
}

.welcome-card p {
  margin-bottom: 0.5rem;
  color: #666;
}

.button-group {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-bottom: 1.5rem;
}

.button-group button {
  background-color: #42b983;
  color: white;
  border: none;
  padding: 0.75rem 1.5rem;
  border-radius: 5px;
  cursor: pointer;
  font-size: 1rem;
  transition: background-color 0.3s;
  margin-bottom: 15px;
}

.button-group button:hover {
  background-color: #226b44;
}

.about-link {
  margin-top: 1rem;
  padding-bottom: 0px;
}

.about-link a {
  color: #42b983;
  text-decoration: none;
  font-weight: bold;
}

.about-link a:hover {
  text-decoration: underline;
  color: #10d5d8;
}

.left-cards, .right-cards {
  position: absolute;
  top: 40%; /* Center vertically */
  transform: translateY(-50%); /* Adjust for centering */
  display: flex;
  flex-direction: column;
  gap: 20px; /* Adds space between cards */
  width: 20%; /* Adjust the width as needed */
}

.left-cards {
  left: 0; /* Align to the left of the screen */
  margin-left: -30%;
}

.right-cards {
  right: 0; /* Align to the right of the screen */
  margin-right: -30%;
}

.card {
  background-color: #ffffff;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  border-radius: 5px;
  padding: 0px;
  text-align: center;
  
}

.card-header {
  margin-bottom: 7px;
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

.temp-icon {
  width: 50px;
  height: 50px;
  margin-right: 10px;
}

.foot {
  margin: 7%;
}
</style>
