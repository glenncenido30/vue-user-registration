<template>
    <div class="container mt-4">
      <h2 class="text-center">Registered Users</h2>
      <transition-group name="fade" tag="ul" class="list-group">
        <li v-for="user in users" :key="user.id" class="list-group-item">
          <strong>{{ user.name }}</strong> - {{ user.email }}
        </li>
      </transition-group>
    </div>
  </template>
  
  <script>
  export default {
    props: ["users"],
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
  