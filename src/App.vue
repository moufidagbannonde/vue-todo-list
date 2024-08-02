<template>
  <div class="contain">
    <h1>Bienvenu(e) dans l'univers des tâches</h1>

    <div class="form-component">
      <FormulaireVue @add-tache="addList" />
      <TableauVue :parentArray = todoArray />

      <div class="contain-table">
        
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import FormulaireVue from "./Components/FormulaireVue.vue";
import TableauVue from "./Components/TableauVue.vue";

let todoArray = ref([]);

const addList = (todos) => {
  todoArray.value = todos.value;
 
};


//Incrémentation et réinitialisation de l'entrée input

//Ajout d'un nouvel élément à notre tableau

//Modification de l'état en fonction du checkbox
// function toggle(todo) {
  // if (todo.etat) {
  //   todoArray.value.map((t) => {
  //     if (t.id == todo.id) t.etat = false;
  //   });
  // } else {
  //   todoArray.value.map((t) => {
  //     if (t.id == todo.id) t.etat = true;
//     });
//   }
// }

//Modification d'un élément


//Suppression d'un élément
function supp(todo) {
  todoArray.value = todoArray.value.filter((t) => t.id !== todo.id);
}
</script>

<style>
/*********** Contain ***********/
.contain {
  width: 800px;
  background-color: white;
  height: 800px;
  text-align: center;
  box-shadow: 5px 5px 2px blueviolet, 10px 10px 2px burlywood,
    -5px -5px 2px burlywood, -10px -10px 2px blueviolet;
}

h1 {
  font-family: Cambria, Cochin, Georgia, Times, "Times New Roman", serif;
  font-size: 2.5em;
  color: burlywood;
  text-decoration: underline;
  width: 90%;
  margin: 0 auto;
}

/*********************************/

 

div.form-component > div.contain-table {
  width: 80%;
}

div.form-component > .div-form {
  width: 50%;
}

div.form-component > div.div-form input {
  width: 80%;
  height: 30px;
  padding-left: 15px;
}

div.form-component > div.div-form button {
  width: 30%;
  height: 20px;
  color: brown;
  font-weight: bold;
  background-color: lavender;
  border: none;
  cursor: pointer;
}

div.form-component > div.div-form button:hover {
  transition: 0.6s;
  transform: scale(1.1);
  color: burlywood;
  background-color: white;
}

.icone-sup svg {
  color: red;
  width: 20px;
}

.icone-up svg {
  color: blue;
  width: 20px;
}

/*********** tableau  ***********/
table {
  border-collapse: collapse;
  border: solid 1px;
  width: 100%;
}

table th,
table td {
  padding-inline: 15px;
  padding-block: 5px;
  border: solid 1px;
}

.form-component {
  display: flex;
  gap: 15px;
  justify-content: center;
  align-items: center;
}

.td-icones {
  display: flex;
  justify-content: space-around;
  border: 1px solid;
}

.td-icones span {
  cursor: pointer;
}
/*********************************/
</style>