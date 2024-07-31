<template>
  <div class="max-w-lg mx-auto p-4 bg-white shadow-md rounded-md form-container">
    <form @submit.prevent="submit()">
      <div class="flex items-center mb-4">
        <img :src="gravatarUrl" alt="Profile Picture" class="w-16 h-16 rounded-full" />
        <div class="ml-4">
          <button class="text-gray-600 hover:text-gray-900" type="button" @click="generateUrl()">
            <i class="fas fa-edit"></i>
          </button>
        </div>
      </div>
  
      <div class="mb-4">
        <label class="block text-gray-700">Full Name</label>
        <div class="flex">
          <input v-model="firstName" type="text" placeholder="First Name" class="mr-2 p-2 border rounded-md w-1/2" required>
          <input v-model="lastName" type="text" placeholder="Last Name" class="p-2 border rounded-md w-1/2" required>
        
        </div>
      </div>
  
      <div class="mb-4">
        <label class="block text-gray-700">Email</label>
        <div class="flex">
          <input v-model="email" type="email" class="p-2 border rounded-md w-full" required>
        </div>
      </div>
  
      <div class="mb-4">
        <label class="block text-gray-700">Password</label>
        <div class="flex">
          <input v-model="password" :type="showPassword ? 'text' : 'password'" class="p-2 border rounded-md w-full" required>
          <button @click="togglePasswordVisibility" type="button" class="text-gray-600 hover:text-gray-900 ml-2">
            <i :class="showPassword ? 'fas fa-eye-slash' : 'fas fa-eye'"></i>
          </button>
  
        </div>
        <div class="mt-2">
          <div class="relative w-full h-2 bg-gray-200 rounded">
            <div :style="{ width: passwordStrength + '%' }" class="absolute top-0 left-0 h-2 bg-green-500 rounded"></div>
          </div>
        </div>
      </div>
      <div class="mt-4">
        <button type="submit" class="px-4 py-2 bg-blue-500 text-white rounded-md hover:bg-blue-700">
          Submit
        </button>
      </div>
    </form>
  </div>
</template>

<script>
import md5 from 'md5';
import zxcvbn from 'zxcvbn';

export default {
  data() {
    return {
      firstName: '',
      lastName: '',
      email: 'user@example.com',
      password: '',
      showPassword: false,
      gravatarUrl: null
    };
  },
  computed: {
    fullName() {
      return `${this.firstName} ${this.lastName}`;
    },
    passwordStrength() {
      return zxcvbn(this.password).score * 25;
    },
  },
  mounted() {
    this.generateUrl();
  },
  methods: {
    submit(){
      alert("Updated!");
    },
    togglePasswordVisibility() {
      this.showPassword = !this.showPassword;
    },
    generateUrl() {
      const hash = md5(this.email.trim().toLowerCase());
      this.gravatarUrl = `https://www.gravatar.com/avatar/${hash}?d=identicon`;
    }
  },
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;600&display=swap');

body {
  font-family: 'Open Sans', sans-serif;
}

.form-container {
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}

</style>
