<template>
  <div class="container mt-5">
    <div id="aqiCarousel" class="carousel slide" data-ride="carousel">
      <ol class="carousel-indicators">
        <li data-target="#aqiCarousel" data-slide-to="0" class="active"></li>
        <li data-target="#aqiCarousel" data-slide-to="1"></li>
        <li data-target="#aqiCarousel" data-slide-to="2"></li>
      </ol>

      <div class="carousel-inner">
        <div class="carousel-item active">
          <div class="card">
            <div class="card-body">
              <h5 class="card-title">City 1</h5>
              <p class="card-text">AQI: {{ aqiData[0].aqi }}</p>
              <p class="card-text">Status: {{ aqiData[0].status }}</p>
            </div>
          </div>
        </div>

        <div class="carousel-item">
          <div class="card">
            <div class="card-body">
              <h5 class="card-title">City 2</h5>
              <p class="card-text">AQI: {{ aqiData[1].aqi }}</p>
              <p class="card-text">Status: {{ aqiData[1].status }}</p>
            </div>
          </div>
        </div>

        <div class="carousel-item">
          <div class="card">
            <div class="card-body">
              <h5 class="card-title">City 3</h5>
              <p class="card-text">AQI: {{ aqiData[2].aqi }}</p>
              <p class="card-text">Status: {{ aqiData[2].status }}</p>
            </div>
          </div>
        </div>
      </div>

      <a class="carousel-control-prev" href="#aqiCarousel" role="button" data-slide="prev">
        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
        <span class="sr-only">Previous</span>
      </a>

      <a class="carousel-control-next" href="#aqiCarousel" role="button" data-slide="next">
        <span class="carousel-control-next-icon" aria-hidden="true"></span>
        <span class="sr-only">Next</span>
      </a>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AqiCarousel',
  data() {
    return {
      aqiData: [
        { city: 'City 1', aqi: 50, status: 'Good' },
        { city: 'City 2', aqi: 100, status: 'Moderate' },
        { city: 'City 3', aqi: 150, status: 'Unhealthy for Sensitive Groups' },
      ],
    };
  },
};
</script>

<style scoped>
.card {
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}
</style>