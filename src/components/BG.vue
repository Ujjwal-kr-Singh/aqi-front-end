
  // In your component
<!-- <template>
  <div :style="{ backgroundImage: `url(${backgroundImage})` }">
     Content of your div 
  </div>
</template> -->
<template>
    <div >
    </div>
  </template>
<script>

// import { mapState } from 'vuex'

export default {
    name: 'BG',

//     computed: {
//     ...mapState(['backgroundImage']),
//   },
//   // ...
};
</script>

<style>
body {
  background-image: url("@/assets/bg/ds.jpg");
  background-repeat: repeat;
  background-attachment:scroll;
  background-size: 123%;
}
</style>