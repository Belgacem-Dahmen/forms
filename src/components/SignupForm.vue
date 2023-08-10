<template>
  <!--
  This example requires some changes to your config:
  
  ```
  // tailwind.config.js
  module.exports = {
    // ...
    plugins: [
      // ...
      require('@tailwindcss/forms'),
    ],
  }
  ```
-->
  <!--
  This example requires updating your template:

  ```
  <html class="h-full bg-white">
  <body class="h-full">
  ```
-->
  <div class="flex min-h-full flex-col justify-center px-6 py-12 lg:px-8">
    <div class="sm:mx-auto sm:w-full sm:max-w-sm">

      <h2 class="mt-10 text-center text-2xl font-bold leading-9 tracking-tight text-gray-900">Sign in to your account</h2>
    </div>

    <div class="mt-10 sm:mx-auto sm:w-full sm:max-w-sm">
      <form class="space-y-6" @submit.prevent="handleSubmit">
        <div>
          <label for="email" class="block text-sm font-medium leading-6 text-gray-900">Email address</label>
          <div class="mt-2">
            <input v-model="email" id="email" name="email" type="email" autocomplete="email" required
              class="block w-full rounded-md border-0 p-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6">
          </div>
        </div>

        <div>
          <div class="flex items-center justify-between">
            <label for="password" class="block text-sm font-medium leading-6 text-gray-900">Password</label>
            <div class="text-sm">
              <a href="#" class="font-semibold text-indigo-600 hover:text-indigo-500">Forgot password?</a>
            </div>
          </div>
          <div class="mt-2">
            
            <input v-model="password" id="password" name="password" type="password" autocomplete="current-password"
              required
              class="block w-full rounded-md border-0 p-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6">
              <p v-if="passwordError" class="text-red-500"> {{ passwordError }}</p>
            </div>
          <div class="mt-2 flex flex-col">
            <label class="mt-5"> Role</label>
            <select class="mt-5" v-model="role">
              <option value="developer">Developer</option>
              <option value="designer">Designer</option>
            </select>
          </div>

          <div class="mt-2 flex flex-col">
            <label class="mt-5"> User : </label>

            <input type="checkbox" value="kacem" v-model="names"><label>kacem</label>
            <input type="checkbox" value="kevin" v-model="names"><label>kevin</label>
            <input type="checkbox" value="rachida" v-model="names"><label>rachida</label>
          </div>


          <div class="mt-2 flex flex-col">
            <label class="mt-5"> skills : </label>

            <input
              class="block w-full rounded-md border-0 p-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
              type="text" v-model="tempSkill" @keyup="addSkill">
            <div v-for="(skill, index) in skills" :key="index">
              <p @click="deleteSkill(skill)"> {{ skill }} </p>

            </div>
          </div>

        </div>

        <div class="mt-2 flex flex-col">


          <div class="flex items-center mb-4">

            <label for="default-checkbox" class="ml-2 text-sm font-medium text-gray-900 dark:text-gray-300">accept Term of
              Use ? </label>
            <input id="default-checkbox" type="checkbox" v-model="terms"
              class=" ml-4 w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 rounded focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600">

          </div>


        </div>



        <div>
          <button
            class="flex w-full justify-center rounded-md bg-indigo-600 px-3 py-1.5 text-sm font-semibold leading-6 text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">Create
            Account </button>
        </div>
      </form>

      <div class="mt-2">
        <p> {{ email }}</p>
        <p> {{ password }}</p>
        <p>{{ role }}</p>
        <p>{{ terms }}</p>
        <p>{{ names }}</p>
        <p>{{ tempSkill }}</p>
        <p> {{ skills }} </p>

      </div>
    </div>
  </div>
</template>

<script>

export default {

  data() {
    return {
      email: '',
      password: '',
      role: 'designer',
      terms: true,
      names: [],
      tempSkill: '',
      skills: [],
      passwordError:''
    }
  },
  methods: {
    addSkill(e) {
      if (e.key === "," && this.skills) {

        if (this.skills.includes(this.tempSkill)) {
          this.tempSkill = ""
        } else {
          this.skills.push(this.tempSkill)
          this.tempSkill = ''
        }
      }
    },
    deleteSkill(skill) {
      this.skills = this.skills.filter((item) => {
        return skill !== item

      })
    },
    handleSubmit() {
      //validatePassword
      this.password.length > 8  ? this.passwordError ='' : this.passwordError ="Password should be more than 8 chars";
      
     
    }
  }
}
</script>


