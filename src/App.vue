<template>
  <div id="app">
    <RegistrationForm @userRegistered="addUser" />
    <UserList :users="users" />
  </div>
</template>

<script>
import axios from "axios";
import RegistrationForm from "./components/RegistrationForm.vue";
import UserList from "./components/UserList.vue";

export default {
  components: { RegistrationForm, UserList },
  data() {
    return {
      users: [],
    };
  },
  methods: {
    async fetchUsers() {
      try {
        const response = await axios.get("https://jsonplaceholder.typicode.com/users");
        this.users = response.data;
      } catch (error) {
        console.error("Error fetching users:", error);
      }
    },
    addUser(newUser) {
      this.users.push({ ...newUser, id: this.users.length + 1 });
    }
  },
  created() {
    this.fetchUsers();
  },
};
</script>

<style>
#app {
  display: flex;
  flex-direction: column;
  align-items: center;
  min-height: 100vh;
  background-color: #f8f9fa;
}
</style>
