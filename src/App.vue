<template>
  <div class="container-fluid py-3 pizarra">
    <div class="row">
      <h1 class="text-center my-3 titulo">Kanban Board</h1>
    </div>
    <div class="row justify-content-center">
      <div class="col-md-4 form">
        <input type="text"
          class="form-control"
          v-model="newTask" 
          placeholder="Add new Task"
          @keypress.enter="add" 
        >
      </div>
      <div class="col-md-2">
        <button class="btn btn-primary ml-2" @click.prevent="add">
          Add Task
        </button>   
      </div>
    </div>
    <div class="row mt-3">
      <div class="col-md-3">
        <div class="p-2 borde">
          <h3 class="subtitulo text-center">Backlog</h3>
          <draggable class="kanban-column" v-model="arrBacklog" group="tasks" @start="drag=true" @end="drag=false" item-key="name">
            <template #item="{element}">
              <div class="col post-it text-center align-items-center">{{element.name}}</div>
            </template>
          </draggable>
        </div>
      </div>
      <div class="col-md-3">
        <div class="p-2 borde">
          <h3 class="subtitulo text-center">In Progress</h3>
          <draggable class="kanban-column" v-model="arrInProgress" group="tasks" @start="drag=true" @end="drag=false" item-key="name">
            <template #item="{element}">
              <div class="post-it text-center align-items-center">{{element.name}}</div>
            </template>
          </draggable>
        </div>
      </div>
      <div class="col-md-3">
        <div class="p-2 borde">
          <h3 class="subtitulo text-center">Tested</h3>
          <draggable class="kanban-column" v-model="arrTested" group="tasks" @start="drag=true" @end="drag=false" item-key="name">
            <template #item="{element}">
              <div class="post-it text-center align-items-center">{{element.name}}</div>
            </template>
          </draggable>
        </div>
      </div>
      <div class="col-md-3">
        <div class="p-2">
          <h3 class="subtitulo text-center">Done</h3>
          <draggable class="kanban-column" v-model="arrDone" group="tasks" @start="drag=true" @end="drag=false" item-key="name">
            <template #item="{element}">
              <div class="post-it text-center align-items-center">{{element.name}}</div>
            </template>
          </draggable>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import draggable from 'vuedraggable';
export default {
  name: 'App',
  components:{
    draggable
  },
  data() {
    return {
      newTask:'',
      drag: false,
      arrBacklog: [
        {name: 'Code SignUp page'},
        {name: 'Test Dashboard'},
        {name: 'Style Registration'},
        {name: 'Help with Designs'},
      ],
      arrInProgress: [],
      arrTested: [],
      arrDone: []
    }
  },
  methods: {
    add(){
      if(this.newTask){
        this.arrBacklog.push({name: this.newTask});
        this.newTask = '';
      }
    }
  },
}
</script>

<style>
.pizarra {
  background-image: url('../public/beige-aged-background.jpg');
  background-size: cover;
  height: 100%;
}

.borde{
  border-right: 6px solid #aaadaa;
}

.titulo{
  font-family: 'Permanent Marker', cursive;
  font-size: 45px;
}
.subtitulo{
  font-family: 'Permanent Marker', cursive;
  font-size: 32px;
  text-decoration: underline;
}

.kanban-column{
  height: 423px;
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-template-rows: repeat(3, 1fr);
  grid-column-gap: 0px;
  grid-row-gap: 0px;
}

.post-it {
  width: 125px;
  height: 125px;
  background-color: #ffff8f;
  font-family: 'Shadows Into Light', cursive;
  font-size: 20px;
  margin: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: grab;
  transform: rotate(-6deg);
  -webkit-transform: rotate(-6deg);
  -o-transform: rotate(-6deg);
  -moz-transform:rotate(-6deg);
}

.post-it:nth-child(even){
  transform: rotate(4deg);
  -o-transform:rotate(4deg);
  -webkit-transform:rotate(4deg);
  -moz-transform:rotate(4deg);
  position:relative;
  top:5px;
  background:rgb(172, 250, 172);
}

.post-it:nth-child(3n){
  transform: rotate(-3deg);
  -o-transform:rotate(-3deg);
  -webkit-transform:rotate(-3deg);
  -moz-transform:rotate(-3deg);
  position:relative;
  top:-5px;
  background:rgb(191, 230, 250);
}
.post-it:nth-child(5n){
  transform: rotate(5deg);
  -o-transform:rotate(5deg);
  -webkit-transform:rotate(5deg);
  -moz-transform:rotate(5deg);
  position:relative;
  top:-10px;
}
</style>
