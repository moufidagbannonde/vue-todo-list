<template>
  <div class="contain">
    <h1>Bienvenu(e) dans l'univers des tâches</h1>

    <div class="form-component">
      <div class="div-form">
        <form @submit.prevent="addList">
          <label for="">Ajoutez une tâche</label>
          <br />
          <input type="text" required v-model="inputValue" />
          <br />
          <button>Ajouter</button>
        </form>
      </div>

      <div class="contain-table">
        <table>
          <thead>
            <tr>
              <th>Avis</th>
              <th>Tâche</th>
              <th>Etat</th>
              <th>Actions</th>
            </tr>
          </thead>
          <tbody v-if="todoArray.length == 0">
            <tr>
              <td colspan="4">En attente de tâches...</td>
            </tr>
          </tbody>
          <tbody v-else>
            <tr v-for="todo in todoArray" :key="todo.id">
              <td>
                <input type="checkbox" @click="toggle(todo)"  :checked="todo.etat"/>
              </td>
              <td>{{ todo.text }}</td>
              <td>{{ !todo.etat ? "non traitée" : "traitée"}}</td>
              <td class="td-icones">
                <span class="icone-up" @click="modif(todo)" v-if="!todo.etat">
                  <svg
                    xmlns="http://www.w3.org/2000/svg"
                    fill="none"
                    viewBox="0 0 24 24"
                    stroke-width="1.5"
                    stroke="currentColor"
                    class="size-6"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      d="m16.862 4.487 1.687-1.688a1.875 1.875 0 1 1 2.652 2.652L6.832 19.82a4.5 4.5 0 0 1-1.897 1.13l-2.685.8.8-2.685a4.5 4.5 0 0 1 1.13-1.897L16.863 4.487Zm0 0L19.5 7.125"
                    />
                  </svg>
                </span>
                <!-- <button>modif</button> -->
                <span class="icone-sup" @click="supp(todo)">
                  <svg
                    xmlns="http://www.w3.org/2000/svg"
                    fill="none"
                    viewBox="0 0 24 24"
                    stroke-width="1.5"
                    stroke="currentColor"
                    class="size-6"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      d="m20.25 7.5-.625 10.632a2.25 2.25 0 0 1-2.247 2.118H6.622a2.25 2.25 0 0 1-2.247-2.118L3.75 7.5m6 4.125 2.25 2.25m0 0 2.25 2.25M12 13.875l2.25-2.25M12 13.875l-2.25 2.25M3.375 7.5h17.25c.621 0 1.125-.504 1.125-1.125v-1.5c0-.621-.504-1.125-1.125-1.125H3.375c-.621 0-1.125.504-1.125 1.125v1.5c0 .621.504 1.125 1.125 1.125Z"
                    />
                  </svg>
                </span>
              </td>
            </tr>
          </tbody>
          <tfoot v-if="todoArray.length !== 0">
            <tr>
              <th colspan="4"></th>
            </tr>
          </tfoot>
        </table>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

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
  console.log(todoArray.value);
  changeValue();
};

function toggle(todo){

  if(todo.etat){
    todoArray.value.map(t => {
    if(t.id == todo.id) 
     t.etat = false;
    });
    console.log(todoArray.value);
  } else {
    todoArray.value.map(t => {
    if(t.id == todo.id) 
     t.etat = true;
    });
   
  }
 
}

function modif(todo) {
  
}

function supp(todo) {
  todoArray.value= todoArray.value.filter(t => t.id !== todo.id);
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

div.form-component {
  display: flex;
  flex-direction: column;
  align-items: center;
}

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

.icone-up svg{
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

.td-icones span{
 cursor: pointer;
}
/*********************************/
</style>