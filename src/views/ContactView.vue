<template>
  <div class="contact">
    <!-- Contact Us Section with Image Background -->
    <div data-aos="fade-down" data-aos-duration="500">
      <div class="contact-header">
        <h1>Contact Us</h1>
      </div>
    </div>
    
    <!-- Contact Information and Form Section -->
    <div class="contact-container">
      <!-- Contact Information Section -->
      <div class="contact-info">
        <p class="intro-text">
          We’re here to assist you in making your home truly beautiful. Whether you need design advice, have inquiries about our products, or require help with an order, please feel free to contact us at any time. Let’s work together to create your ideal space!
        </p>
        <div class="info-section">
          <div class="office-info">
            <h3>OUR OFFICE</h3>
            <h4>Address</h4>
            <p class="intro-text">
              Micasa Home Decor<br>
              The Decor Hub, 12 Bree Street<br>
              Cape Town, 8000<br>
              South Africa
            </p>
            <br>
            <h4>Contact Number</h4>
            <p class="intro-text">+27 21 123 4567</p>
            <br>
            <h4>Email Us</h4>
            <p class="intro-text">contact@micasahome.co.za</p>
            <br>
            <h4>Office Hours</h4>
            <p class="intro-text">
              Monday to Friday: 9:00 AM – 6:00 PM<br>
              Saturday: 10:00 AM – 4:00 PM<br>
              Sunday: Closed
            </p>
            <br>
          </div>
        </div>
      </div>

      <!-- Contact Form Section -->
      <div class="contact-form">
        <h2>Any Questions?</h2>
        <p class="intro-text">Use the form below to get in touch with us.</p>
        <form @submit.prevent="handleSubmit">
          <label for="name">Your Name </label>
          <input type="text" id="name" v-model="form.name" placeholder="Write your name here" required>
  
          <label for="email">Your Email </label>
          <input type="email" id="email" v-model="form.email" placeholder="Write your email here" required>
  
          <label for="phone">Phone Number</label>
          <input type="tel" id="phone" v-model="form.phone" placeholder="Write your phone number">
  
          <label for="subject">Subject </label>
          <input type="text" id="subject" v-model="form.subject" placeholder="Write your subject here" required>
  
          <label for="message">Your Message </label>
          <textarea id="message" v-model="form.message" placeholder="Write your message here" required></textarea>
  
          <button type="submit">Submit</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
// Import SweetAlert2
import Swal from 'sweetalert2';

export default {
  data() {
    return {
      form: {
        name: '',
        email: '',
        phone: '',
        subject: '',
        message: '',
      },
    };
  },
  methods: {
    async handleSubmit() {
      // Custom validation
      if (!this.form.name || !this.form.email || !this.form.subject || !this.form.message) {
        Swal.fire({
          title: 'Validation Error',
          text: 'Please fill out all required fields.',
          icon: 'error',
          confirmButtonText: 'OK',
        });
        return;
      }

      try {
        const response = await fetch('https://formcarry.com/s/NQsKj4W9e2L', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
            'Accept': 'application/json',
          },
          body: JSON.stringify(this.form),
        });

        // Debugging response
        console.log('Response Status:', response.status);
        console.log('Response Status Text:', response.statusText);
        const responseText = await response.text();
        console.log('Response Text:', responseText);

        if (response.ok) {
          Swal.fire({
            title: 'Success',
            text: 'Your message has been sent successfully.',
            icon: 'success',
            confirmButtonText: 'OK',
          });
          this.resetForm();
        } else {
          Swal.fire({
            title: 'Submission Error',
            text: 'There was an error submitting your message. Please try again later.',
            icon: 'error',
            confirmButtonText: 'OK',
          });
          console.error('Error response:', response.status, response.statusText, responseText);
        }
      } catch (error) {
        Swal.fire({
          title: 'Network Error',
          text: 'There was a problem with your submission. Please try again later.',
          icon: 'error',
          confirmButtonText: 'OK',
        });
        console.error('Network error:', error);
      }
    },
    resetForm() {
      this.form.name = '';
      this.form.email = '';
      this.form.phone = '';
      this.form.subject = '';
      this.form.message = '';
    },
  },
};
</script>

<style scoped>
/* Add your styling here */
</style>
