<template>
  <div class="mainSignUp">
    <div class="header">
      <div class="header-description">
        <h3 class="header-title blink">¿ Que esperas?</h3>
        <p class="header-subtitle">¡Comienza a organizarte!</p>
      </div>
    </div>

    <form @submit.prevent="signUp" class="form-sign-up">
      <div class="form">
        <div class="form-input">
          
          <input
            type="email"
            class="form-input-field"
            placeholder="example@gmail.com"
            id="email"
            v-model="email"
            required
          />
        </div>
        <div class="form-input">  
          <input
            type="password"
            class="form-input-field"
            placeholder="**********"
            id="password"
            v-model="password"
            required
          />
        </div>
        <div class="form-input">
          <input
            type="password"
            class="form-input-field"
            placeholder="**********"
            id="confirmPassword"
            v-model="confirmPassword"
            required
          />
        </div>
        <button class="signUp-button">
    Sign up
    <div class="signUp-button-wrapper">
        <div class="signUp-button-arrow"></div>

    </div>
</button>
        <p class="registrate">
          Have an account?
          <PersonalRouter
            :route="route"
            :buttonText="buttonText"
            class="link-registrate"
          />
        </p>
      </div>
    </form>

    <div v-show="errorMsg">{{errorMsg}}</div>
  </div>
</template>

<script setup>

import { ref, computed } from "vue";
import PersonalRouter from "./PersonalRouter.vue";
import { supabase } from "../supabase";
import { useRouter } from "vue-router";
import { useUserStore } from "../stores/user";
import { storeToRefs } from "pinia";
// Route Variables
const route = "/auth/login";
const buttonText = "Sign In";
// Input Fields
const email = ref("");
const password = ref("");
const confirmPassword = ref("");
// Error Message
const errorMsg = ref("");
// Router to push user once SignedUp to Log In
const redirect = useRouter();
const signUp = async () => {
  if (password.value === confirmPassword.value) {
    try {
      await useUserStore().signUp(email.value, password.value);
      redirect.push({ path: "/auth/login" });
    } catch (error) {
      errorMsg.value = error.message;
      setTimeout(() => {
        errorMsg.value = null;
      }, 5000);
    }
    return;
  }
  errorMsg.value = "error";
};
</script>

<style></style>
