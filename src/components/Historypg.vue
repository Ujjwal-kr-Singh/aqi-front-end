<template>
  <div class="boodi">
    <div class="page">
      <div class="history-page">
        <h1>Search History</h1>
        <div v-if="result && result.success"> 
          <div class="card-container">
            <div class="card" v-for="(search, index) in searchHistory" :key="index">
              <div class="city-name">
                <h2>{{ search.cityName.toUpperCase() }}</h2>
              </div>
              <div class="aqi">
                <p>Overall AQI: {{ search.overall_aqi }}</p>
              </div>
              <div class="time">
                <p>{{ new Date(search.createdAt) }}</p>
              </div>
            </div>
          </div>
        </div>
        <div v-else>
          <div class="empty-container" v-if="result && !result.success">
            <p>No search history found. Please login to view your history.</p>
          </div>
          <div v-else>
            <p>Loading...</p> </div>
        </div>
      </div>
      <div class="bottom"></div>
    </div>
  </div>
</template>

<script>
import Swal from 'sweetalert2';
import axios from 'axios';
// import router from '@/router'; // Assuming you have a router setup

export default {
  name: 'HistoryPage',
  data() {
    return {
      searchHistory: [],
      result: null,
    };
  },
  created() {
    this.loadSearchHistory();
  },

  methods: {
    async loadSearchHistory() {
      try {
        let result = await axios({
          method: 'get',
          url: 'http://localhost:3000/searchistory',
          withCredentials: true // Ensure cookies are sent with the request
        });

        this.result = result.data; // Store the entire response data

        if (this.result.success) {
          this.searchHistory = this.result.data.slice().reverse();
        } else {
          // Show the SweetAlert for login prompt
          Swal.fire({
            title: 'Login Required',
            text: 'Please login to view your search history.',
            icon: 'warning',
            confirmButtonText: 'Okay',
          }).then(() => {
            // Optionally redirect to login page here
            // router.push({ path: '/login' });
          });
        }
      } catch (e) {
        console.log(e.message, "error");
        this.result = null; // Set result to null to handle the loading state
      }
    },
  },
};
</script>

<style scoped>
.history-page {
  padding: 20px;
}

.card-container {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.card {
  display: flex;
  color: rgb(255, 255, 255);
  justify-content: space-between;
  align-items: center;
  padding: 20px;
  border-radius: 10px;
  background-color: transparent;
  box-shadow: 15px 15px 15px 20px;
  max-width: 75%;
  margin-left: 14%;
  margin-bottom: 1rem;
}

.city-name {
  font-size: 1.2em;
  font-weight: bold;
}
h1 {
  color: rgb(235, 252, 0);
}
.bottom {
  margin: 10rem;
}
.boodi {
  background-image: url('@/assets/bg/R (2).jpg');
  background-repeat: repeat;
  background-attachment: scroll;
  background-size: 100%;
  max-height: 1000%;
}
.page {
  max-width: 100%;
  max-height: 100%;
  background-color: transparent;
  overflow: hidden;
  transition: all 0.3s ease-in-out;
}
.empty-container {
  margin: 0; /* Reset margin */
  padding: 20px; /* Add padding for content spacing */
  background-size: cover; /* Cover the entire area */
  text-align: center;
  font-size: 1.7em;
  text-transform: capitalize;
  text-decoration:wavy;
  color: #fff;
  display: flex; /* Use flexbox for centering */
  align-items: center; /* Center vertically */
  justify-content: center; /* Center horizontally */
  height: 70vh; /* Make the container full height */
  flex-direction: column; /* Arrange content vertically */
}
.empty-container .hover{
  font-size: 3em;
}




</style>