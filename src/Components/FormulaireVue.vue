<template>
    <div class="div-form">
        <form @submit.prevent="addList">
          <h1 for="">Ajoutez une tâche</h1>
          <br />
          <input type="text" required v-model="inputValue" id="inputTache"/>
          <br />
          <button @click="toggle(todo)" id="ajouterBtn">Ajouter</button>
        </form>
    </div>
</template>
<script setup>
import { ref } from "vue";

const emit = defineEmits(["add-tache"]);
let id = ref(0);
let todoArray = ref([]);
let inputValue = ref("");


function changeValue() {
    id.value++;
  inputValue.value = "";
}

const addList = function () {
    todoArray.value.push({
    id: id.value,
    text: `${inputValue.value}`,
    etat: false,
  });
  
  emit ('add-tache', todoArray)
  changeValue();
};
// console.log(changeValue);
// console.log(todoArray.value);
    

</script>

<style scoped>
div h1 {
    color: red;
}
</style>