<script setup>
import axios from "axios";
import { ref } from "vue";
import Swal from "sweetalert2";
const email = ref("");

const instance = axios.create({
  baseURL: "http://192.168.1.4:5000",
  timeout: 3000,
});
function submitEmail(e) {
  e.preventDefault();
  instance
    .post("/subscribers", {
      email: email.value,
    })
    .then(function (response) {
      Swal.fire(response.data.message, "", "success");
      email.value = "";
    })
    .catch(function (error) {
      console.log(error);
    });
}
</script>

<template>
  <div class="grid gap-5 grid-cols-1 w-full p-5 lg:p-0 lg:grid-cols-2">
    <div
      class="flex lg:m-5 flex-col py justify-between border-2 border-black h-full p-5"
    >
      <div
        class="bg-purple-300 rounded-t-full flex flex-col justify-evenly py-18 items-center h-full"
      >
        <h1
          class="text-xl sm:font-bold sm:text-2xl sm:uppercase relative my-16"
        >
          <span class="relative z-50 font-serif">Coming Soon!</span>
          <span
            class="z-10 absolute bottom-[-5px] right-[-20px] h-[16px] w-[110px] bg-[#DBAF00]"
          ></span>
        </h1>
        <h1
          class="text-xl text-center w-[90%] sm:text-center sm:leading-loose font-bold font-serif sm:text-5xl uppercase"
        >
          Get Notified When We Lunch
        </h1>
        <form class="ml-3 my-5 sm:flex justify-between" @submit="submitEmail">
          <input
            id="email"
            type="email"
            placeholder="Enter your email"
            class="w-[90%] mx-2 sm:mx-0 outline-none sm:w-[100%] p-1 px-3 sm:p-2 sm:px-10"
            v-model="email"
          />
          <button
            type="submit"
            class="w-[90%] mx-2 bg-purple-700 text-white sm:mx-0 sm:w-[50%] sm:py-2 px-8 sm:mr-4 uppercase my-3 p-1 sm:my-0"
          >
            submit
            <i class="inline-block justify-between fa fa-arrow-right"></i>
          </button>
        </form>
      </div>
    </div>
    <div>
      <img src="/images/desktop.svg" alt="" class="hidden sm:block" />
      <img src="/images/mobile.svg" alt="" class="sm:hidden" />
    </div>
  </div>
</template>

<style>
body {
  background: rgb(236, 236, 236);
  background: linear-gradient(
    90deg,
    rgba(236, 236, 236, 1) 0%,
    rgba(207, 206, 227, 1) 100%
  );
}
@tailwind base;
@tailwind components;
@tailwind utilities;
</style>
