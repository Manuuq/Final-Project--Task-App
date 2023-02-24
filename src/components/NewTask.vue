<template>
  <div class="container-task">
    <div class="div1">
      <h1>
        <div>
          ¡<span class="underlined-text">Create</span> your
          <span class="underlined-text"></span> tasks <br />
        </div>
        <div>
        
        </div>
      </h1>
       
      <div v-if="showErrorMessage">
        <p class="error-text">{{ errorMessage }}</p>
      </div>
    </div>

    <div class="div2">
      <!-- input animado -->
      <div class="group">
        <input required="" type="text" v-model="name" class="input" />
        <span class="highlight"></span>
        <span class="bar"></span>
        <label class="animation1">Título de la tarea</label>
      </div>

      <div class="group">
        <input required="" type="text" v-model="description" class="input" />
        <span class="highlight"></span>
        <span class="bar"></span>
        <label class="animation2">Descripción de la tarea</label>
      </div>
    </div>

    <div class="div 3">
      <button @click="addTask" class="fancy">
        <span class="top-key"></span>
        <span class="text">Añadir tarea</span>
        <span class="bottom-key-1"></span>
        <span class="bottom-key-2"></span>
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { useTaskStore } from "../stores/task";
import { supabase } from "../supabase";
const taskStore = useTaskStore();
// variables para los valors de los inputs
const name = ref("");
const description = ref("");
// constant to save a variable that holds an initial false boolean value for the errorMessage container that is conditionally displayed depending if the input field is empty
const showErrorMessage = ref(false);
// const constant to save a variable that holds the value of the error message
const errorMessage = ref(null);
const emit = defineEmits(["addTitle"]);
// Arrow function para crear tareas.
const addTask = () => {
  if (name.value.length < 4 || description.value.length < 4) {
    // Primero comprobamos que ningún campo del input esté vacío y lanzamos el error con un timeout para informar al user.
    showErrorMessage.value = true;
    errorMessage.value =
      "Te falta introducir un título y descripción de tu tarea o es muy corto";
    setTimeout(() => {
      showErrorMessage.value = false;
    }, 5000);
  } else {
    // Aquí mandamos los valores a la store para crear la nueva Task. Esta parte de la función tenéis que refactorizarla para que funcione con emit y el addTask del store se llame desde Home.vue.
    taskStore.addTask(name.value, description.value);
    name.value = "";
    description.value = "";
    //Función que hace que se refresque la lista de tareas.
    //Aquí hacemos el emit. Home recibirá el emit y llamará a la función getTask().
    emit("addTitle");
  }
};
</script>
  
  <style>
  .container-task {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin-bottom: 5vw;
    border: solid 1px red;
  }
  
  .container-task2 {
    display: flex;
    flex-direction: column;
    justify-content: center;
    border: solid 1px red;
  }
  
  .container-task h1 {
    margin-top: 5vw;
  }
  .error-text {
    font-size: 0.8vw;
  }
  
  .input-field input {
    width: 75vw;
    height: 5vh;
    margin-top: 2.5vh;
    margin-bottom: 2.5vh;
    border-radius: 1vw;
    border-width: 0.1vw;
    padding-left: 2vw;
  }
  
  .button {
    margin-top: 2.5vh;
    height: 5vh;
  }
  
  .input-field:last-of-type input {
    height: 15vh;
  }
  </style>
    