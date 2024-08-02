<template>
  <div class="form-component">
    <table>
      <thead>
        <tr>
          <th>Avis</th>
          <th>Tâche</th>
          <th>Etat</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody v-if="parentArray.length == 0">
        <tr>
          <td colspan="4">En attente de tâches...</td>
        </tr>
      </tbody>
      <tbody v-else>
        <tr v-for="todo in parentArray" :key="todo.id">
          <td>
            <input type="checkbox" v-model="todo.etat" />
          </td>
          <td>{{ todo.text }}</td>
          <td>{{ !todo.etat ? "Non traitée" : "Traitée" }}</td>
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
      <tfoot v-if="parentArray.length !== 0">
        <tr>
          <th colspan="4"></th>
        </tr>
      </tfoot>
    </table>
  </div>
</template>

<script setup>
import { ref } from "vue";
// let parentArray = ref([]);
const prop = defineProps({
  parentArray: Array,
});
function modif(todo) {
  let newText = prompt('Modifier la tâche', todo.text);
  if (newText !== null && newText.trim() !== '') {
    todo.text = newText;
  }
}




// function toggle(todo) {
//   if (todo.etat) {
//     parentArray.value.map((t) => {
//       if (t.id == todo.id) {
//         t.etat = false;
//       } else {
//         parentArray.value.map((t) => {
//           if (t.id == todo.id) t.etat = true;
//         });
//       }
//     });
//   }
// }
</script>

<style>
</style>