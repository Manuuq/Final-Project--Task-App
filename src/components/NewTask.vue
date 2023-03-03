<template>
  <div class="container-task">
    <div class="div1">
      <h1>
        <div>
          <span class="underlined-text">Crea</span> 
          <span class="underlined-text"> Tareas </span><br />
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
        
        <span class="text">Añadir tarea</span>
       
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
const showErrorMessage = ref(false);
// const constant to save a variable that holds the value of the error message
const errorMessage = ref(null);
const emit = defineEmits(["addTitle"]);
// Arrow function para crear tareas.
const addTask = () => {
  if (name.value.length < 4 || description.value.length < 4) {
    showErrorMessage.value = true;
    errorMessage.value =
      "Te falta introducir un título y descripción de tu tarea o es muy corto";
    setTimeout(() => {
      showErrorMessage.value = false;
    }, 5000);
  } else {
    taskStore.addTask(name.value, description.value);
    name.value = "";
    description.value = "";
    emit("addTitle");
  }
};
</script>
  
  <style>
  </style>
    