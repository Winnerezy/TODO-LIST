<script setup>
import { ref } from 'vue';
let inputs = ref([]); //intialize the text array as
let textInput = ref(''); //initialize the text input as empty string

//method to add text to the array
const addText = () =>{
if(textInput.value.trim() == ""){ //if no input nothing will occur
return
} 
else{ //if input is added add the input to the array
inputs.value.push(textInput.value);
textInput.value  = ""; //input value becomes empty string
}

}
let complete = ref(0) //initializing the complete value and assigning it to 0
const completed = (index)=>{
  complete.value++ //incrementing the completed task number
  inputs.value.splice(index, 1)
}

//method to delete text
const del = (index) =>{
    inputs.value.splice(index, 1) //delete the text with index of the current index 
}
</script>

<template>
    <section id="main">
    <header>
        <input type="text" @keydown.enter="addText" v-model="textInput">
    </header>
    <div id="completedCount">
        <div>{{ complete }} Taks Completed</div>
    </div>
    
    <ul v-for="(input, index) in inputs" :key="index">
    <div>
            <li>{{ input }}</li>
            <button @click="del(index)">Delete</button>
            <input type="checkbox" name="completed" id="completed" @click="completed">
    </div>
</ul>
  
    </section>
      
</template>

<style scoped>

header{
    display: flex;
    align-items: center;
    justify-content: baseline;
}

#completedCount{
    font-family: Arial;
    font-weight: bold;
    align-items: start;
    justify-content: center;
    display: flex;
    border: none;
}

#main{
    position: relative;
    top: 50px;
}

input{
    width: 300px;
    outline: transparent;
    border-radius: 15px;
    height: 25px;
}

ul{
    display: flex;
    align-items: center;
    justify-content: center;
    list-style-type: none;
    padding: 0;
}
div{
    display: flex;
    align-items: center;
    justify-content: center;
    column-gap: 10px;
    color: white;
    font-size: 15px;
    border: 2px solid white;
    padding: 15px;
    border-radius: 10px;
    max-width: 350px;
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