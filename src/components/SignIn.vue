<!-- COMPONENTE BOILERPLATE -->

<template>
  <div class="main">
    <div class="app">
      <h3>TO-DO APP</h3>
      <p class="empezamosText">¿Empezamos?</p>

      
      <form @submit.prevent="signIn">
        <div>
          <input placeholder="Enter your Email" required="" type="email" v-model="email" class="input-mail-password" />
          <label  for="email"></label>
        </div>

        <div>
          <input placeholder="Password" type="password" v-model="password" class="input-mail-password" />
          <label for="password"></label>
        </div>
        <div>
          <button data-text="Ingresar" class="button-signIn">
            <span class="actual-text">&nbsp;Ingresar&nbsp;</span>
            <span class="hover-text" aria-hidden="true"
              >&nbsp;Ingresar&nbsp;</span>
          </button>
         
          <p class="registrate">
            ¿ Aun no te has registrado?
            <PersonalRouter
              :route="route"
              :buttonText="buttonText"
              class="link-registrate"
            />
          </p>
        </div>
      </form>
    </div>
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
const route = "/auth/signup";
const buttonText = "¡Registrate!";
// Input Fields
const email = ref("");
const password = ref("");
// Error Message
const errorMsg = ref("");
// Router to push user once SignedUp to Log In
const redirect = useRouter();
// Login Function
const signIn = async () => {
  try {
    await useUserStore().signIn(email.value, password.value);
    redirect.push({ path: "/" });
  } catch (error) {
    errorMsg.value = `Error: ${error.message}`;
    setTimeout(() => {
      errorMsg.value = null;
    }, 2500);
  }
};
</script>

<style scoped>
</style>