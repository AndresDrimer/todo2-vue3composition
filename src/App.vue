<script setup>
import { ref, onMounted } from "vue";

const nuevaTarea = ref("");

const tareas = ref([]);

const sumarTarea = () => {
  if (nuevaTarea.value != "") {
    tareas.value.push({ done: false, content: nuevaTarea.value });
    nuevaTarea.value = "";
    localStorage.setItem("tareas", JSON.stringify(tareas)); //esto no lo pude hacer andar
  }
};

const borrarEntrada = () => {
  nuevaTarea.value = "";
};

function toggleDone(tarea) {
  tarea.done = !tarea.done;
  
}

function deleteTask(tarea) {
  tareas.value.splice(nuevaTarea.value, 1);
}

// const vMyDirective = {
// beforeMount: (data) => { l
// let data = localStorage.getItem("tareas");
// if (data != null) {
// tareas = JSON.parse(data);

// do something with the element

//created(()=>{
//let data = localStorage.getItem("tareas");
//if (data != null) {
//  tareas = JSON.parse(data);
//
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
        
        <button type="submit" @click.prevent="sumarTarea" class="btn-mini">
          <img src="./assets/check-box-svgrepo-com.svg" alt="check" />
        </button>
        <button type="reset" @click.prevent="borrarEntrada" class="btn-mini">
          <img src="./assets/cross-sign-svgrepo-com.svg" alt="reset" />
        </button>
      </form>

      <div class="row">
        <div class="col-sm-12">
          <div class="card" v-for="tarea in tareas" :key="tarea">
            <div class="card-body" :class="{ done: tarea.done }">
              <h3 class="card-title">{{ tarea.content }}</h3>
              
      
              <button
                class="whiteBck"
                
                @click.prevent="toggleDone(tarea)"
              > <img  src="./assets/thumbs-up-svgrepo-com (1).svg" :class="{ greyish: tarea.done }">
               
              </button>
              <button
                v-show="tarea.done"
                class="whiteBck"
                @click.prevent="deleteTask(tarea)"
              >
                <img src="./assets/trash-svgrepo-com (1).svg" class="btn-mini" alt="">
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
  text-decoration: line-through;
}

.wrapper {
  margin: 5rem auto;
  border: 2px solid black;
  border-radius: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  background-color: whitesmoke;
  padding: 10px;
  max-width: 80vw;
}
@media (max-width: 700px) {
  .wrapper {
    width: 90vw;
  }
}
button{
   border: none;
}
button img {
  width: 1rem;
 
}
.btn-mini {
  border: none;
  background: none;
  cursor: pointer;
}
.card {
  min-width: 290px;
  margin-top: -1rem;
  max-width: 400px;
  margin: auto;
  max-height: fit-content;
}
.card-body {
  max-width: 100%;
  display: flex;

}
.row {
  min-width: 40vw;
}
form {
  min-width: 30vw;
}
.card-title{
  padding-right: 20px;
  margin: auto;
}
.whiteBck{
  background-color: white;
}
.greyish{
  -webkit-filter: grayscale(100%);
        filter: grayscale(100%);
}
</style>
