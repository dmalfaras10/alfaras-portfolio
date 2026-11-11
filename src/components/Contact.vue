<script setup>
    import {ref, onMounted, onBeforeUnmount} from 'vue'
    import {Notyf} from 'notyf'
    import axios from 'axios'
    import 'notyf/notyf.min.css';

    const notyf = new Notyf();
    const WEB3FORM_ACCESS_KEY = "d5770afc-3565-49ea-a740-41f304c6aabc";
    const SITE_KEY = "6LdBrxouAAAAAE56w1972uhtHjSy5DBYgvOKuBMP";
    const first_name = ref("");
    const last_name = ref("");
    const email = ref("");
    const phone = ref("");
    const subject = ref("");
    const company = ref("");
    const message = ref("");
    const isLoading = ref(false);

    const submitForm = async() => {
    	if (!recaptchaToken.value) {
    	    notyf.error('Please verify that you are not a robot.');
    	    return;
    	}

        isLoading.value = true

        try{
            const response = await axios.post("https://api.web3forms.com/submit",{
                access_key : WEB3FORM_ACCESS_KEY,
                first_name : first_name.value,
                last_name : last_name.value,
                email : email.value,
                phone : phone.value,
                subject : subject.value,
                company : company.value,
                message : message.value
            }, {
                headers : {
                    'Content-Type' : "application/json",
                    Accept : "application/json"
                }
            }
        )

        const result = response.data;

        if(result.success){
            notyf.success("Message Sent!");
            first_name.value = "";
            last_name.value = "";
            email.value = "";
            phone.value = "";
            subject.value = "";
            company.value = "";
            message.value = "";
        }

        }catch (e){
            notyf.error("Failed to send email!")
        }finally{
            isLoading.value = false
        }

    }

  	const recaptchaContainer = ref(null);
    const recaptchaWidgetId = ref(null);
    const recaptchaToken = ref('');

    // Callback called by reCAPTCHA when successful
    function onRecaptchaSuccess(token) {
      recaptchaToken.value = token;
    }

    // Callback when expired
    function onRecaptchaExpired() {
      recaptchaToken.value = '';
    }

    // Function to render the reCAPTCHA widget
    function renderRecaptcha() {
      if (!window.grecaptcha) {
        console.error('reCAPTCHA not loaded');
        return;
      }

      recaptchaWidgetId.value = window.grecaptcha.render(recaptchaContainer.value, {
        sitekey: SITE_KEY,
        size: 'normal', // or 'compact'
        callback: onRecaptchaSuccess,
        'expired-callback': onRecaptchaExpired,
      });
    }

    // Function to reset reCAPTCHA 
    function resetRecaptcha() {
      if (recaptchaWidgetId.value !== null) {
        window.grecaptcha.reset(recaptchaWidgetId.value);
        recaptchaToken.value = '';
      }
    }



    onMounted(() => {
      // This code waits for the Google reCAPTCHA library to load, then renders the reCAPTCHA widget using onMounted hook. 
      // The widget is rendered with grecaptcha.render(), which requires a sitekey. 
      // Callback functions handle success and expiration events. 
      // reCAPTCHA is reset upon form submission to clear the token.
      const interval = setInterval(() => {
        if (window.grecaptcha && window.grecaptcha.render) {
          renderRecaptcha();
          clearInterval(interval);
        }
      }, 100);

      onBeforeUnmount(() => {
        clearInterval(interval);
      });
    });

</script>

<template>
	<div class="row text-center p-2 p-lg-5" id="contact">
	  <h1 class="py-5" id="title">Get in Touch</h1>
	  <div class="col-12 col-lg-8 p-5 mx-auto" id="form-container">
	    <form @submit.prevent="submitForm">
	      <!-- First Name & Last Name -->
	      <div class="row">
	        <div class="col-12 col-md-6 mb-4 text-start">
	          <label for="first-name" class="form-label">First Name</label>
	          <input type="text" class="form-control"  id="first-name" name="first_name" placeholder="Enter your first name" required v-model="first_name">
	        </div>
	        <div class="col-12 col-md-6 mb-4 text-start">
	          <label for="last-name" class="form-label">Last Name</label>
	          <input type="text" class="form-control" id="last-name" name="last_name" placeholder="Enter your last name" required v-model="last_name">
	        </div>
	      </div>
	      <!-- Email -->
	      <div class="mb-4 text-start">
	        <label for="email" class="form-label">Email</label>
	        <input type="email" class="form-control" id="email" name="email" placeholder="email@example.com" required v-model="email">
	      </div>
	      <!-- Phone -->
	      <div class="mb-4 text-start">
	        <label for="phone" class="form-label">Phone Number</label>
	        <input type="tel" class="form-control" id="phone" name="phone" placeholder="+63 912 345 6789" required v-model="phone">
	      </div>
	      <!-- Subject -->
	      <div class="mb-4 text-start">
	        <label for="subject" class="form-label">Subject</label>
	        <input type="text" class="form-control" id="subject" name="subject" placeholder="What is this about?" required v-model="subject">
	      </div>
	      <!-- Company / Organization -->
	      <div class="mb-4 text-start">
	        <label for="company" class="form-label">
	          Company / Organization
	          <span class="text-muted">(Optional)</span>
	        </label>
	        <input type="text" class="form-control" id="company" name="company" placeholder="Company name" required v-model="company">
	      </div>
	      <!-- Message -->
	      <div class="mb-4 text-start">
	        <label for="message" class="form-label">Message</label>
	        <textarea class="form-control" id="message" name="message" rows="6" placeholder="Enter your message"required v-model="message"></textarea>
	      </div>
	      <!-- Submit -->
	      <button type="submit" class="btn w-100"id="send-message" :disabled="isLoading">{{ isLoading ? "Sending...": "Subbmit"}}</button>
	      <!-- recaptcha checkbox -->
	      <div class="d-flex justify-content-center mt-3">
	          <div ref="recaptchaContainer"></div>
	      </div>    
	    </form>
	  </div>
	</div>	
</template>