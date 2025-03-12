<template>
  <div class="container mt-5">
    <h2 class="text-center mb-4">User Registration</h2>

    
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

      <button type="submit" class="btn btn-primary" :disabled="loading">
        <span v-if="loading">Submitting...</span>
        <span v-else>Register</span>
      </button>
    </form>

    <hr />

    
    <h3>Registered Users</h3>
    <div v-if="loading">Loading users...</div>
    <transition-group name="fade" tag="ul" class="list-group">
      <li v-for="user in users" :key="user.id" class="list-group-item">
        <strong>{{ user.name }}</strong> - {{ user.email }}
      </li>
    </transition-group>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      user: {
        name: "",
        email: "",
        password: "",
        age: "",
      },
      users: [], 
      errors: {},
      loading: false, 
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
    
    async registerUser() {
      if (this.validateForm()) {
        try {
          this.loading = true; 

          
          await axios.post("https://jsonplaceholder.typicode.com/users", this.user);

          alert("User registered successfully!");
          
          
          this.fetchUsers();
        } catch (error) {
          console.error("Error submitting form:", error);
        } finally {
          this.loading = false; 
        }
      }
    },

    async fetchUsers() {
      try {
        this.loading = true;
        const response = await axios.get("https://jsonplaceholder.typicode.com/users");
        this.users = response.data;
      } catch (error) {
        console.error("Error fetching users:", error);
      } finally {
        this.loading = false;
      }
    }
  },
  
  mounted() {
    this.fetchUsers(); 
  }
};
</script>

<style>

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>
