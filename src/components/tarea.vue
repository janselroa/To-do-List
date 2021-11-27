<template>
    <div class="task" :class="{'complet':complet}">
        <div @click="complet_tasks" class="complet-check">
            <i class="material-icons">done</i>
        </div>
        <div class="tasks__content">
            <h2>{{title}}</h2>
            <p>{{description}}</p>
        </div>
        <span @click="$emit('deleteTask')" class="material-icons close">
            close
        </span>
        
    </div>
</template>
<script>
export default {
    props:['title','description','complet'],
    methods:{
        complet_tasks(){
            this.complet=!this.complet;
            this.$emit('complet_tasks')
        }
    },
}
</script>
<style scoped>
.task{
    width:350px;
    padding:10px;
    margin:20px;
    background-color: hsla(0, 0%, 20%, 0.807);
    color:#fff;
    border-radius: 10px;
    display: flex;
}
.task h2{
    margin:0;
}
.tasks__content{
    width:300px;
    overflow-y: auto;
}
.complet{
    opacity: 0.8;
}
.complet .complet-check{
    background-color:rgb(163, 229, 255);
    color: hsla(0, 0%, 20%);
}
.complet-check{
    width:30px;
    height:30px;
    margin-right: 20px;
    display: flex;
    justify-content:center;
    align-items:center;
    color:transparent;
    border: 1px solid #aaa;
    font-size:1.3rem;
    border-radius: 20px;
    cursor: pointer;
}
.task:hover{
    background-color: hsla(0, 0%, 20%, 0.860);
}
.close{
    display: inline-block;
 font-size:1.7rem;
}
</style>