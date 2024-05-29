<script setup>
import { ref } from 'vue'
const boxes = ref([]);
const text = ref("");
const showPopup = ref(false);

const createBox = () => {
  
  showPopup.value = true;
};
const closePopup = () => {
  
  boxes.value.push(text.value);
  text.value = '';
      showPopup.value = false;
};

</script>

<template>
  <div class = "popup-container" v-if ="showPopup">
    <div class = "popup">
      <div class="popup-content">
         <slot>
          <input class = "popup-textbox" placeholder = "write task here" v-model="text">

          <button class = "popup-button" @click="closePopup">Add Task</button>
        </slot>
      </div>
    </div>
  </div>
  <button class="task-button" @click="createBox" >
    <span class="task-button-icon"></span>
  </button>

<div class="flex-parent">
    <div class="flex-container">
      <div class ="task-box-titles">To-Do</div>
      <div v-for="(box, index) in boxes" :key="index" class="box">{{ box }}</div>
    </div>
    <div class="flex-container">
      <div class ="task-box-titles">Working</div>
  </div>
  
    <div class="flex-container">
      <div class ="task-box-titles">Done</div>
  </div>
    </div>

</template>

<style scoped>

.flex-parent {
  display: flex;
  flex-direction: row; 
  height: 80%;
  width: 100%;
  padding: 10% 10% 0% 10%;
}
.flex-container {

  display: flex;
  flex-direction: column; 
  border: solid black 2px;
  border-radius: 10px;
  width: 100%;
}
.task-box-titles {
  align-self: center;
}

.flex-parent > div:not(:first-child) {
  border-left: unset;
}

.task-button {
    background: #7616e3;
    border-color: rgba(0, 0, 0, 0);
    color: #000000;
    border-radius: 50%;
    height: 4em;
    line-height: 1;
    width: 4em;

    position: relative;
    top: 18%;
    left: 5%;
    
}

.task-button-icon::before {
    content: '\00002B';
    font-size: 50px;
    width: auto;
    
}

.popup-container {
  position: fixed;
  top: 10;
  left: 10;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5); /* semi-transparent overlay */
  display: flex;
  justify-content: center;
  align-items: center;
}

.popup {
  background-color: white;
  padding: 250px;
  border-radius: 20px;
}

.popup-button {
  
}


  

</style>
