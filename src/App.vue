<template>
  <div id="app">
    <div class="settings">

        <span @click="settingsActive" class="material-icons settings-icon">
            settings
        </span>

      <div v-if="settingsActivated" class="theme-segttins">
        <div @click="changeTheme('black')"></div>
        <img @click="changeTheme('ocean')" src="@/assets/ocean.jpg" alt="ocean">
        <img @click="changeTheme('nature')" src="@/assets/nature.jpg" alt="nature">
        <img @click="changeTheme('city')" src="@/assets/city.jpg" alt="city">
      </div>
    </div>
<div class="card-input">
    <input type="text" v-model="newTask.title" placeholder="Title">
    <input type="text" v-model="newTask.description" placeholder="Description">
    <button @click="createTasks">Create Task</button>
</div>
<div class="tasks">
    <tarea v-for="(task,$index) in listTasks" :key="$index" :title="task.title" :description="task.description" :complet="task.complet"
      @complet_tasks="complet_tasks($index)"
    ></tarea>
    </div>
    
    <footer class="footer">Created By Jansel Roa 2021 &copy;<a href="http://github.com/janselroa" target="_blank">Janselroa</a> </footer>
  </div>
</template>
<script>
import tarea from "@/components/tarea.vue";
export default {
  name: 'App',
  components: {
    tarea,
  },
  created(){
    const body = document.body;
    body.classList.add('ocean')
    if(localStorage.getItem('listTasks')){
      this.listTasks=JSON.parse(localStorage.getItem('listTasks'));
    }
  },
  data(){
    return {
      listTasks:[
        {
          title:'Example',
          description:`
              Lorem ipsum dolor sit amet, consectetur adipisicing elit`
        },{
          title:'Example',
          description:`
              Lorem ipsum dolor sit amet, consectetur adipisicing elit`
        }
      ],
      newTask:{},
      settingsActivated:false,
      theme:"ocean",
    }
  },
  methods: {
    createTasks(){
      if(this.newTask.title!=null){
          this.newTask.complet=false;
          this.listTasks.unshift(this.newTask);
          localStorage.setItem("listTasks", JSON.stringify(this.listTasks));
          this.newTask={};
      }
    },
    complet_tasks(index){
      if(this.listTasks[index].complet) this.listTasks[index].complet=false; 
      else this.listTasks[index].complet=true;
       localStorage.setItem("listTasks", JSON.stringify(this.listTasks));
    },
    settingsActive(){
      console.log("asd")
      this.settingsActivated=!this.settingsActivated;
      console.log(this.settingsActived)
    },
    changeTheme(theme){
      const body = document.body;
      body.classList.replace(this.theme,theme)
      this.theme=theme;
    }
  }
}
</script>

<style lang="scss">
@font-face {
  font-family: 'Material Icons';
  font-style: normal;
  font-weight: 400;
  src: url(https://example.com/MaterialIcons-Regular.eot); /* For IE6-8 */
  src: local('Material Icons'),
    local('MaterialIcons-Regular'),
    url(https://example.com/MaterialIcons-Regular.woff2) format('woff2'),
    url(https://example.com/MaterialIcons-Regular.woff) format('woff'),
    url(https://example.com/MaterialIcons-Regular.ttf) format('truetype');
}

body{
  height:100vh;
  font-family:'Roboto';
  background-size: cover;
  background-repeat:no-repeat;
}
.ocean{
  background-image:url("assets/ocean.jpg") !important;
}

.nature{
  background-image: url("assets/nature.jpg") !important;
}
.city{
  background-image:url("assets/city.jpg") !important;
}
.black{
  background: #222 !important;
}
#app{
  color:#fff;
  height:100vh;
  display: flex;
  flex-direction: column;
}
.card-input{
  width:400px;
  margin: 100px auto;
  input{
    display:block;
    width:100%;
    background-color: hsla(0, 0%, 20%, 0.856);
    color:#fff;
    margin: 10px 0;
  }
  input,button{
    border: none;
    outline: none;
    padding:12px;
  }
  button{
    display: block;
    width:100px;
    margin: auto;
    color:#fff;
    background-color: #222;
  }
}
.tasks{
  width:100%;
  margin:100px 0;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
.settings{
  font-size:2.3rem;
  width:400px;
  position:absolute;
  top: 50px;
  right: 20px;
}
.settings span{
  font-size:2.3rem;
  position: absolute;
  top:-30px;
  right: 20px;
}
.theme-segttins{
  width:400px;
  height: 200px;
  display: flex;
  flex-wrap: wrap;
  position: absolute;
  top:20px;
  background-color:#333;
  overflow-y: auto;
  img{
    width:150px;
    height:100px;
    object-fit: cover;
    margin: 5px;
  }
  div{
    width:150px;
    height: 100px;
    margin: 5px;
    background-color:#222;

  }
  img:hover,div:hover{
    outline: 1px solid #ddd;
  }
}
.footer{
  margin-top: auto;
  text-align: center;
}
.footer a{
  color:inherit;
}
</style>
