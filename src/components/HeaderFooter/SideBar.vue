<template>
    <head>
        <meta charset="utf-8">
        <title>CourseList</title>
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
    </head>
    <body>
        <div class="sidebocs">  
         <span>
          <button class="btn btn-warning custom-btn" type="button" data-bs-toggle="offcanvas" data-bs-target="#demo"> <b>≡</b></button>
      </span>
        </div>
    <div class="offcanvas offcanvas-start text-bg-dark" id="demo">
        <div class="offcanvas-header">
          <h1 class="offcanvas-title">Quick Links</h1>
          <button type="button" class="btn-close btn-close-white" data-bs-dismiss="offcanvas"></button>
        </div>
        <div class="offcanvas-body">
            <nav>
              <b><router-link to="/">Welcome</router-link></b><br/><br/>

              <b><router-link to="/SignUp">SignUp</router-link></b><br/><br/>
              <b><router-link to="/login">Login </router-link></b><br/><br/>

                <b><router-link to="/front3">Get Started</router-link></b><br/><br/>
                <!-- <b><router-link to="/front"></router-link></b><br/><br/> -->
                <b><router-link to="/NewFront">Api-Search</router-link></b><br/><br/>

                <b><router-link to="/HomePage2">Server Search</router-link></b><br/><br/>
                <b><router-link to="/HistoryPg">History</router-link></b><br/><br/>
                <!-- <b><router-link to="/HistoryPage">History</router-link></b><br/><br/> -->

                <!-- <b><router-link to="/FrontExtra">FrontExtra</router-link></b><br/><br/> -->
              </nav><nav class="xtra">
                <b><router-link to="/MyAdvisory">Advisory</router-link></b><br/><br/>
              <i><b><router-link to="/TempView">*TempView</router-link></b></i><br/><br/>
                <i><b><router-link to="/TempSearch">*TempSearch</router-link></b></i><br/><br/>
 
 


              </nav> 

         
          <!-- <button class="btn btn-secondary" type="button">A Button</button> -->
        </div>
      </div>
      </body>   
   
</template>
<script>

import 'bootstrap/dist/css/bootstrap.min.css'
import 'bootstrap/dist/js/bootstrap.bundle.min.js'
export default {
     
    name:"SideBar",

}
</script>
<style>
.sidebar {
    width: 1px; /* Adjust width as needed */
    padding: 1px; /* Adjust padding as needed */
    padding-top: 1px; /* Adjust padding as needed */
  }
  
  .btn btn- custom-btn{
    /* Optional styling for the button */
    background-color: rgb(18, 255, 129);
    width: auto; /* Adjust width as needed */
    height: auto; /* Adjust height as needed */
    border: none;
    font-size: 30px;
    margin-left: 0px;
    border-radius: 7px; /* Adjust border-radius as needed */
    transition: background-color 0.3s ease; /* Add transition for smooth hover effect */
    background-image: none;
    
  }
  
  /* Hover effect */
  .sidebar .custom-btn:hover {
    background-color: #e20d0d; /* Change background color on hover */
    border: black;
    gap: 1rem;
    cursor: pointer; /* Change cursor to pointer on hover */
  }
  .offcanvas{
    width: 100%;
    background-color:rgb(0, 0, 0);
    transition: 1s;
    padding-top: 0px;
    background-blend-mode: color-burn;
  }
       
  .sidebocs{
    background-color: black;
  }
  .custom-btn:hover {
    background-color: #08df45; /* Change background color on hover */
    border: black;
    gap: 1rem;
    cursor: pointer; /* Change cursor to pointer on hover */ 
  }
  .xtra{
    color: #ffffff;
  }
  

</style>