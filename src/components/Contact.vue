<template>
	<div class="row text-center p-2 p-lg-5" id="contact">
	  <h1 class="py-5" id="title">Get in Touch</h1>
	  <div class="col-12 col-lg-8 p-5 mx-auto" id="form-container">
	    <form>
	      <!-- First Name & Last Name -->
	      <div class="row">
	        <div class="col-12 col-md-6 mb-4 text-start">
	          <label for="first-name" class="form-label">First Name</label>
	          <input type="text" class="form-control"  id="first-name" name="first_name" placeholder="Enter your first name" required>
	        </div>
	        <div class="col-12 col-md-6 mb-4 text-start">
	          <label for="last-name" class="form-label">Last Name</label>
	          <input type="text" class="form-control" id="last-name" name="last_name" placeholder="Enter your last name" required>
	        </div>
	      </div>
	      <!-- Email -->
	      <div class="mb-4 text-start">
	        <label for="email" class="form-label">Email</label>
	        <input type="email" class="form-control" id="email" name="email" placeholder="email@example.com" required
	        >
	      </div>
	      <!-- Phone -->
	      <div class="mb-4 text-start">
	        <label for="phone" class="form-label">Phone Number</label>
	        <input type="tel" class="form-control" id="phone" name="phone" placeholder="+63 912 345 6789">
	      </div>
	      <!-- Subject -->
	      <div class="mb-4 text-start">
	        <label for="subject" class="form-label">Subject</label>
	        <input type="text" class="form-control" id="subject" name="subject" placeholder="What is this about?" required>
	      </div>
	      <!-- Company / Organization -->
	      <div class="mb-4 text-start">
	        <label for="company" class="form-label">
	          Company / Organization
	          <span class="text-muted">(Optional)</span>
	        </label>
	        <input type="text" class="form-control" id="company" name="company" placeholder="Company name">
	      </div>
	      <!-- Message -->
	      <div class="mb-4 text-start">
	        <label for="message" class="form-label">Message</label>
	        <textarea class="form-control" id="message" name="message" rows="6" placeholder="Enter your message"required
	        ></textarea>
	      </div>
	      <!-- Submit -->
	      <button type="submit" class="btn w-100"id="send-message">
	        Send Message
	      </button>
	    </form>
	  </div>
	</div>	
</template>