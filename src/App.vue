<script setup>

import { ref, onMounted } from "vue";

const nuevaTarea = ref("");

const tareas = ref([]);

const sumarTarea = () => {
  if (nuevaTarea.value != "") {
    tareas.value.push({ done: false, content: nuevaTarea.value });
    console.log(tareas.value);
    nuevaTarea.value = "";
    localStorage.setItem("tareas", JSON.stringify(tareas));
  }
};

const borrarEntrada = () => {
  nuevaTarea.value = "";
};

function toggleDone(tarea) {
  tarea.done = !tarea.done;
  console.log("toggle done");
}

function deleteTask(tarea) {
  tareas.value.splice(nuevaTarea.value, 1);
}

onMounted (() => {
let data = localStorage.getItem("tareas");
if (data != null){
  tareas = JSON.parse(data)
}
});

</script>

<template>
  <main>
    <div class="wrapper">
      <h1>TO-DO LIST</h1>
      <form>
        <input
          type="text"
          v-model="nuevaTarea"
          name="nuevaTarea"
          placeholder="add task"
          autofocus
        />
        <button type="reset" @click.prevent="borrarEntrada" class="btn-mini"> <img src="./assets/cross-sign-svgrepo-com.svg" alt="reset"> </button>
        <button type="submit" @click.prevent="sumarTarea" class="btn-mini"> <img src="./assets/check-box-svgrepo-com.svg" alt="check"> </button>
      </form>

      <div class="row">
        <div class="col-sm-12">
          <div class="card" v-for="tarea in tareas" :key="tarea">
            <div class="card-body" :class="{ done: tarea.done }">
              <h3 class="card-title">{{ tarea.content }}</h3>
              <button
                v-show="!tarea.done"
                class="btn btn-primary"
                @click.prevent="toggleDone(tarea)"
              >
                completed
              </button>
              <button
                v-show="tarea.done"
                class="btn btn-danger"
                @click.prevent="deleteTask(tarea)"
              >
                delete
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>


<style scoped>

h1 {
  text-align: center;
}
form {
  margin-bottom: 2rem;
  padding-top: 1rem;
}
.done {
  background-color: grey;
}

.wrapper{
  width: 50vw;
  margin: 5rem auto ;
  border: 2px solid black;
  border-radius: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  background-color: whitesmoke;
  padding: 10px;
}
@media (max-width: 700px){
  .wrapper{
  width: 80vw;
  }}

button img{
  width: 1.5rem;
  

  }
.btn-mini{
border: none;
background: none;
}
.card{
  width: 40vw;
}
</style>
