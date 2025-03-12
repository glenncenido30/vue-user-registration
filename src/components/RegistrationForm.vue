<template>
    <div class="container mt-5">
      <h2 class="text-center">User Registration</h2>
      <form @submit.prevent="registerUser">
        
        <div class="mb-3">
          <label class="form-label">Name</label>
          <input type="text" class="form-control" v-model="user.name" />
          <small class="text-danger" v-if="errors.name">{{ errors.name }}</small>
        </div>
  
        
        <div class="mb-3">
          <label class="form-label">Email</label>
          <input type="email" class="form-control" v-model="user.email" />
          <small class="text-danger" v-if="errors.email">{{ errors.email }}</small>
        </div>
  
        
        <div class="mb-3">
          <label class="form-label">Password</label>
          <input type="password" class="form-control" v-model="user.password" />
          <small class="text-danger" v-if="errors.password">{{ errors.password }}</small>
        </div>
  
        
        <div class="mb-3">
          <label class="form-label">Age</label>
          <input type="number" class="form-control" v-model="user.age" />
          <small class="text-danger" v-if="errors.age">{{ errors.age }}</small>
        </div>
  
        
        <button type="submit" class="btn btn-primary">Register</button>
      </form>
    </div>
  </template>

<script>
export default {
  data() {
    return {
      user: {
        name: "",
        email: "",
        password: "",
        age: "",
      },
      errors: {},
    };
  },
  methods: {
    validateForm() {
      this.errors = {};

      if (this.user.name.length < 3) {
        this.errors.name = "Name must be at least 3 characters long.";
      }

      const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      if (!emailPattern.test(this.user.email)) {
        this.errors.email = "Enter a valid email address.";
      }

      if (this.user.password.length < 6) {
        this.errors.password = "Password must be at least 6 characters.";
      }

      if (!this.user.age || this.user.age < 18) {
        this.errors.age = "Age must be a number and greater than 18.";
      }

      return Object.keys(this.errors).length === 0;
    },
    registerUser() {
      if (this.validateForm()) {
        alert("Form is valid! Submitting...");
        
      }
    },
  },
};
</script>

  