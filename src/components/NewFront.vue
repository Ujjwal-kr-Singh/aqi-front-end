<template>
  <body>
    <div class="container1">
      <!-- <div class="pict">
        <img src="@/assets/aqi1n.jpg" alt="img not found" />
      </div> -->
      <div class="container">
        <h1 class="title">Air Quality Index</h1>
        <div class="search-bar">
          <input type="text" v-model="searchQuery" placeholder="Enter your location" />
          <button @click="searchLocation">Search</button>
        </div>
        <div class="index">
          <p1>Status: {{ getStatus(aqi) }}</p1>
          <div class="aqi-circle" :style="aqiCircleStyle">
            {{ aqi }}
          </div>
        </div>
        <div v-if="isLoading" class="loading">
          Loading...
        </div>
        <div v-else-if="error" class="error">
          {{ error }}
        </div>
        <div v-else class="data">
          <div class="location">
            <h2>{{ location }}</h2>
          </div>
          <div class="index">
            <h2>Air Quality Index: {{ aqi }}</h2>
          </div>
          <div class="details">
            <div class="pollutant-card" v-for="(value, key) in pollutants" :key="key">
              <div class="pollutant-icon">{{ getPollutantIcon(key) }}</div>
              <div class="pollutant-info">
                <h3>{{ key }}</h3>
                <p>{{ value }}</p>
              </div>
            </div>
          </div>
          <div class="chart" :style="{ backgroundImage: `url(${getImage(aqi)})` }">
            <h2>{{ aqi }}</h2>
            <!-- <p>Status: {{ getStatus(aqi) }}</p> -->
          </div>
        </div>
        <div class="botom"></div>
      </div>
    </div>
  </body>
</template>

<script>
import axios from 'axios';
export default {
  name: 'NewFront',
  data() {
    return {
      searchQuery: '',
      isLoading: false,
      error: null,
      location: '',
      aqi: null,
      pollutants: {}
    };
  },
  methods: {
    searchLocation() {
      this.isLoading = true;
      this.error = null;
      const apiUrl = "https://api.api-ninjas.com/v1/airquality?city=";
      axios
        .get(apiUrl + this.searchQuery, {
          headers: {
            'X-Api-Key': 't+O/4XAQnZ9NUcDswHrLnw==2f5ebMbPzv0PA47r'
          }
        })
        .then(response => {
          this.location = this.searchQuery;
          this.aqi = response.data.overall_aqi;
          this.pollutants = response.data;
          this.isLoading = false;
        })
        .catch(errorapi => {
          this.error = errorapi.message;
          this.isLoading = false;
        });
    },
    getStatus(aqi) {
      if (aqi === null) {
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
    getImage(aqi) {
      if (aqi === null) return require('@/assets/nodata.jpg');
      if (aqi <= 50) return require('@/assets/clean_sky.jpg');
      if (aqi <= 100) return require('@/assets/moderatepp.jpg');
      if (aqi <= 150) return require('@/assets/sensitivep.jpg');
      if (aqi <= 200) return require('@/assets/highlyp.jpg');
      if (aqi <= 300) return require('@/assets/exremep.jpg');
      return require('@/assets/hazardousp.jpg');
    },
    getPollutantIcon(pollutant) {
      const icons = {
        'PM2.5': '🌫️',
        PM10: '🌁',
        NO2: '💨',
        SO2: '🌋',
        O3: '🌐',
        CO: '🚗',
        overall_aqi:'🌍',
      };
      return icons[pollutant] || '❓';
    }
  
  },
  
  computed: {
    aqiCircleStyle() {
      let backgroundColor;
      if (this.aqi === null) {
        backgroundColor = 'transparent';
      } else if (this.aqi <= 50) {
        backgroundColor = '#00e400';
      } else if (this.aqi <= 100) {
        backgroundColor = '#ffff00';
      } else if (this.aqi <= 150) {
        backgroundColor = '#ff7e00';
      } else if (this.aqi <= 200) {
        backgroundColor = '#ff0000';
      } else if (this.aqi <= 300) {
        backgroundColor = '#8f3f97';
      } else {
        backgroundColor = '#7e0023';
      }
      return {
        backgroundColor,
        color: '#fff'  // Ensures text is visible
      };
    }
  }
};
</script>
<style scoped>
.container1 {
  text-align: center;
  background-image: url('@/assets/cop.avif');
  background-size: cover;
  background-repeat: no-repeat;
  background-attachment: scroll;
  max-height: 120%;
}

.pict {
  width: 100%;
  height: 0vh; /* Adjust height to fit your requirement */
  z-index: 0; /* Ensure background is behind content */
  opacity: 0.7;
  margin-left: -30%;
  object-fit:fill; /* Ensures the image covers the entire container */
}

.container {
  color: #000000;
  padding: 20px;
  overflow:visible; /* Ensure the content flows correctly around the floated image */
  align-items: center;
  margin-top: 0%;
  margin-bottom: 0%;
  z-index: 2;
}

.title {
  font-size: 2em;
  margin-bottom: 1em;
  margin-top: 5rem;
}

.search-bar {
  margin-bottom: 1em;
}

.loading {
  font-size: 1.5em;
}

.error {
  color: red;
  font-size: 1.5em;
}

.data {
  margin-top: 1em;
}

.location h2,
.index h2 {
  margin: 0.5em 0;
}

.details {
  display: flex;
  flex-wrap: nowrap;
  justify-content: center;
  gap: 1em;
  margin-top: 1em;
  overflow-x: auto; /* Allows horizontal scrolling if needed */
  box-shadow: #000000 20px 20px 20px #000000;
  transition: transform 0.3s ease, box-shadow 0.3s ease; /* Add transition for smooth animation */
}
.details:hover {
  transform: scale(1.05); /* Slightly scale up the container on hover */
  box-shadow: #000000 20px 20px 30px #000000; /* Increase the shadow on hover */
}

.pollutant-card {
  background-color: rgba(255, 255, 255, 0.1);
  border: 1px solid #ccc;
  border-radius: 8px;
  padding: 1em;
  min-width: 150px;
  text-align: center;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.pollutant-icon {
  font-size: 2em;
  margin-bottom: 0.5em;
}

.pollutant-info h3 {
  margin: 0;
  font-size: 1.2em;
}

.pollutant-info p {
  margin: 0.5em 0 0;
}

.chart {
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center;
  padding: 20px;
  border-radius: 10px;
  margin-top: 1em;
  margin-left: 0%;
  min-height: 15rem;
}

.aqi-circle {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.5em;
  margin: 20px auto; /* Center horizontally and add some spacing */
}

.botom {
  margin: 35%;
}
p1{
  color: aliceblue;
  font-size: 1.5em;
  text-align: end;
}
</style>