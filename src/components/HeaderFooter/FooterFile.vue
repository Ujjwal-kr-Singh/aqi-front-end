<template>
    <footer class="footer ">
      <div class="container">
        <div class="row">
          <div class="col-md-12 text-center">
            <p class="mb-0">|© {{ new Date().getFullYear() }}| {{ appName }}.<br> All rights reserved by students.</p>
            <p  class="text">A helpful project for better understanding of environment.</p>  
            <!-- <a href="#" class="text-muted">Terms of Service</a> -->
          </div>
        </div>
      </div>
      
    </footer>
  </template>
  
  <script>
  export default {
    name: 'FooterFile',
    data() {
      return {
        appName: 'RD Engineering College Project', // Replace with your app name
      }
    }
  };
  </script>
  
  <style scoped>
  .footer {
    margin-top: 10rem;
    background-color: #f5f5f5;
    padding: 30px 15px;
    padding-bottom: 15px;
    position: fixed; /* Make it fixed */
    bottom: 0;      /* Place it at the bottom of the viewport */
    left: 0;       /* Extend it to the full width */
    width: 100%;    /* Full width */
    z-index: 10;   /* Ensure it stays on top */
    background:scroll;
    color: aliceblue;
  }
  
  .container {
    max-width: 1200px;
    margin: 0 auto;
    margin-top: 0rem;
  }
  
  .text-muted {
    color: #888;
    text-decoration: none;
  }
  
  .text-muted:hover {
    text-decoration: underline;
  }
  </style>