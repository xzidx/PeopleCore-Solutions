<template>
    <div class="flex justify-center items-center w-[100%] h-screen">
    <div class="bg-white w-110 p-8 shadow-md border rounded-lg w-[700px]">
      <h3 class="text-2xl font-bold mb-6 text-center">Login</h3>

      <form @submit.prevent="handleLogin" class="space-y-4">

        <div class="flex justify-center items-center gap-4">
          <input class="w-full p-3 border rounded-lg"
            v-model="name"
            type="text"
            placeholder="Last Name"
            required
          />
          <input class="w-full p-3 border rounded-lg"
            v-model="firstName"
            type="text"
            placeholder="First Name"
            required
          />

        </div>

        <input class="w-full p-3 border rounded-lg"
          v-model="email"
          type="email"
          placeholder="Your Email or number phone"
          required
        />
        <input class="w-full p-3 border rounded-lg"
          v-model="password"
          type="password"
          placeholder="Password"
          required
        />
      

        
        <button class="w-full bg-blue-600 text-white p-3 rounded-lg" type="submit">
            Sign Up
        </button>
    </form>


      <p class="text-sm text-center mt-4">
        Already have an account?
        <NuxtLink to="/sign-up" class="text-blue-600">Make Account</NuxtLink>
      </p>
    </div>
  </div>


  <div>
    <div v-for="data in loginDatas"> 
      {{ data.id }}
      {{ data.bora }}
      {{ data.email }}
    </div>
  </div>
</template>


<script setup>
    import axios from 'axios'
    const config = {
        headers:{
            Authorization: 'Bearer 2bfe23d4a769ff7f237e880cc8bb03933075b1260a562bad4b94bcee0d33639fa7643554ee49eca4ae020350ffa21ce7c2440b21a4f527c92cfb6eb8f2edfa0cba91d1efa7449acbd375ab39d1a1d5cdbccb5387808a4471a23811b66087a938709c0589e94820629d2032b470ef3d0dbc74b4ed82ccd5e267e9f9be5e6cb62f'
        }
    }
    const fetchData = await axios.get('http://localhost:1337/api/logins', config);
    const loginDatas = fetchData.data.data;
    
    console.log(loginDatas);
</script>