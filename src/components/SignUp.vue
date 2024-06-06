<template>
  <div class="signupbocs">
    <div class="container mt-5">
      <h1 class="mb-4 text-center">Sign Up</h1>
      <form @submit.prevent="handleSubmit">
        <div class="form-group">
          <label for="firstName">First Name:</label>
          <input type="text" class="form-control" id="firstName" v-model="firstName" required>
        </div>
        <div class="form-group">
          <label for="lastName">Last Name:</label>
          <input type="text" class="form-control" id="lastName" v-model="lastName" required>
        </div>
        <div class="form-group">
          <label for="city">City:</label>
          <input type="text" class="form-control" id="city" v-model="city" required>
        </div>
        <div class="form-group">
          <label for="phone">Phone Number:</label>
          <input type="tel" class="form-control" id="phone" v-model="phone" required>
        </div>
        <div class="form-group">
            <label for="email">email:</label>
            <input type="email" class="form-control" id="email" v-model="email" required>
          </div>
        <div class="form-group">
          <label for="password">Password:</label><br>
          <input type="password" class="form-control" id="password" v-model="password" required>
        </div>
        <br />
        <button type="submit" class="btn btn-primary">Sign Up</button>
      </form>
    </div>
    </div>
  </template> 
  
  <script>
  import axios from 'axios';
  import router from '@/router';
  export default {
    data() {
      return {
        firstName: '',
        lastName: '',
        city: '',
        phone: '',
        email: '',
        password: '',
      };
    },
    methods: {
        async  handleSubmit() {
        // Here, you would send the collected data to your backend server
        // for user registration.
        
        let data = {
            firstName:this.firstName,
            lastName:this.lastName,
            city:this.city,
            phone:this.phone,
            email:this.email,
            password:this.password,
                }
        let result = await axios({
                method:'post',
                url:'http://localhost:3000/user/create',
                data: data,
              });
              console.log("result", result);
              // console.log("city;ssss id  ",result.data.data.id);
            if (result.data.success) {
                router.push('/') 
      }
        console.log("Submitted Data:", this.firstName, this.lastName, this.city, this.phone, this.password);
      },
    },
  };
  </script>
  
  <style scoped>
  /* You can add additional styling here as needed, but 
     Bootstrap will provide the basic layout and appearance. */
  form-group {
    table-layout: auto;
    margin-left: 50% ;
    margin-right: 50% ;
    tab-size: 10px;

  }
  input {
    width: 50%;
    margin: auto;
    position:sticky;


  }
  .signupbocs{
    border: 1px solid black;
    border-radius: 15%;
    margin: auto;
    background-color:whitesmoke;
    padding-bottom: 1.5% ;
    margin-top: 1.5%;
    box-shadow: 0px 10px 10px 10px;
    width: 30%; 
    margin-bottom: 7.5%;

  }
</style>