<template>
  <div class="hero">
    <h3>Coming soon!</h3>
    <h2>Our Brand New<br>Website is on its way</h2>
    <h4>Subscribe for more details.</h4>
    <form @submit.prevent="submitForm" ref="formRef">
      <input id="inputField" type="email" name="Email" placeholder="Enter your email" v-model="email" required>
      <!-- <input type="number" name="Number" placeholder="Enter yourNumber"> -->
      <button type="submit"><img class="SendIcon" src="../assets/send-icon.png" alt="Send Icon"></button>
    </form>
    <span v-if="showThankYouMessage">Thank you for subscribing</span>
  </div>
 
</template>

<style scoped>
.hero {
  background-image: linear-gradient(rgba(0, 0, 0, 0.8), rgba(0, 0, 0, 0.8)), url("../assets/background.png");
  background-position: center;
  background-size: cover;
  padding: 10px 10%;
  color: #fff;
  height: 70vh;
  width: 50vh;
  object-fit: cover;
}

.hero h2 {
  font-weight: 800;
  font-size: 34px;
}

.SendIcon {
  height: 12px;
  width: 24px;
  border-radius: 8px;
}

input {
  padding: 15px;
  border-radius: 2px;
  border: 0;
}

button {
  padding: 15px;
  background-color: rgb(73, 116, 8);
  border: 0;
}

span {
  color: green;
  display: none; /* Hide initially */
}
.ProductCards{
  text-align: center;
}
</style>

<script setup>

import { ref } from 'vue';

const email = ref('');
const showThankYouMessage = ref(false);
const formRef = ref(null); // Declare a ref for the form

const scriptURL = 'https://script.google.com/macros/s/AKfycbx4Q5MIoJkxEoTc6oGDMHDf_GP4VD8bPwnwv-bF7qJT3EVLxn8secwL9kkVTTZPJsDQUg/exec';

const submitForm = () => {
  const form = formRef.value; // Access the form using the ref
  fetch(scriptURL, {
    method: 'POST',
    body: new FormData(form)
  })
    .then(response => {
      console.log('Success!', response);
      showThankYouMessage.value = true; // Show the thank you message
    })
    .catch(error => console.error('Error!', error.message));
};
</script>



