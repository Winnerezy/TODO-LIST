<script setup>
import { ref } from 'vue';
let inputs = ref([]);
let completedCheck = ref(0)

const storedTasks = localStorage.getItem('storedTasks') //store the tasks in the browser
const storedCompletedCount = localStorage.getItem('storedCompletedCount');
if(storedTasks && storedCompletedCount){
    inputs.value = JSON.parse(storedTasks)
    console.log(inputs.value)
    completedCheck.value =  parseInt(storedCompletedCount)
}

let textInput = ref(''); //initialize the text input as empty string

//method to add text to the array
const addText = () =>{
if(textInput.value.trim() == ""){ //if no input nothing will occur
return
} 
else{ //if input is added add the input to the array
inputs.value.push(textInput.value);
textInput.value  = ""; //input value becomes empty string
localStorage.setItem('storedTasks', JSON.stringify(inputs.value))
}
}


const completed = (index) =>{
    completedCheck.value++
    inputs.value.splice(index, 1)
    localStorage.setItem('storedCompletedCount', completedCheck.value)
    localStorage.setItem('storedTasks', JSON.stringify(inputs.value))
}
//method to delete text
const del = (index) =>{
    inputs.value.splice(index, 1) //delete the text with index of the current index 
}
</script>
<template>
    <header>
        <input type="text" @keydown.enter="addText" v-model="textInput">

        <div id="completedCount">
        <div>{{ completedCheck }} Tasks Completed</div>
        </div>
    </header>


<ul id="tasks">
    <div v-for="(input, index) in inputs" :key="index" :class="{'completed': input-completed}" id="singleTask" style="max-width: 350px;">
            <li>{{ input }}</li>
            <button @click="del(index)">Delete</button>
            <input type="radio" id="completed" @change="completed(index)">
    </div>
</ul>

</template>

<style scoped>

header{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}

#completedCount{
    display: flex;
    font-family: Arial;
    font-weight: bold;
    border: none;
    align-items: center;
    justify-content: center;
    border: 2px solid white;
    padding: 10px;
    border-radius: 10px;
    margin-top: 30px;
    margin-bottom: 30px;
    width: 200px
}

input{
    width: 300px;
    outline: transparent;
    border-radius: 15px;
    height: 25px;
}

#tasks{
    display: grid;
    grid-template-columns: auto auto auto ;
    gap: 10px
}

ul{
    display: flex;
    align-items: center;
    justify-content: center;
    list-style-type: none;
    padding: 0;
}

#singleTask{
    display: flex;
    align-items: center;
    justify-content: center;
    column-gap: 10px;
    color: white;
    font-size: 15px;
    border: 2px solid white;
    padding: 15px;
    border-radius: 10px;
}

li{
    max-width: 200px;
}

button{
    border: none;
    background-color: white;
    height: 20px;
    font-family: 'Arial';
    border-radius: 10px;
}

#completed{
    margin: 0;
    width: 20px;
    height: 20px;
    border:none
}
</style>