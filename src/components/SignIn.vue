<!-- COMPONENTE BOILERPLATE -->

<template>
  <div class="main">
    <div class="app">
      <h3>TO-DO APP</h3>
      <p class="empezamosText">¿Empezamos?</p>

      <!-- inputs nuevos!!!!!!!!!!! -->
      <form @submit.prevent="signIn">
        <div class="signIn">
          <input placeholder="Enter your Email" required="" type="email" v-model="email" class="input" />
          <span class="highlight"></span>
          <span class="bar"></span>
          <label  for="email"></label>
        </div>

        <div class="passInput">
          <input placeholder="Password" type="password" v-model="password" class="input" />
          <span class="highlight"></span>
          <span class="bar"></span>
          <label for="password"></label>
        </div>
        <div>
          <button data-text="Awesome" class="button">
            <span class="actual-text">&nbsp;Ingresar&nbsp;</span>
            <span class="hover-text" aria-hidden="true"
              >&nbsp;Ingresar&nbsp;</span
            >
          </button>
          <!--<button class="fancy" type="submit">
              boton animado 
            <span class="top-key"></span>
            <span class="text">Iniciar Sesión</span>
            <span class="bottom-key-1"></span>
            <span class="bottom-key-2"></span> 
          </button> -->

          <p class="registrate">
            ¿ Aun no te has registrado?
            <PersonalRouter
              :route="route"
              :buttonText="buttonText"
              class="linkRegistrate"
            />
          </p>
        </div>
      </form>
    </div>
  </div>
  <!-- </div> -->
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
/* @import url(../assets/style.css); */
.main {
  background-image: url("");
  background-size: cover;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.container {
  background: rgba(255, 255, 255, 0.5);
  border-radius: 15%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 95vh;
}

.container h3 {
  font-size: 2vw;
  margin-top: 2.5vw;
  margin-bottom: 1.5vw;
}

.container p {
  padding-left: 20vw;
  padding-right: 20vw;
  margin-bottom: 1.5vw;
}

.form {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.form-input input {
  width: 40vw;
  height: 3vw;
  margin-top: 1.5vw;
  margin-bottom: 1.5vw;
  border-radius: 0.7vw;
  border: 0vw;
  padding-left: 3vw;
  padding-top: 1vw;
  padding-bottom: 1vw;
}

.registrarse {
  background-color: black;
  color: white;
  margin-top: 1.5vw;
  margin-bottom: 1.5vw;
  width: 40vw;
  height: 3vw;
  border-radius: 0.7vw;
  border: 0vw;
}

.registrarse:hover {
  background-color: rgb(68, 105, 175);
}
</style>