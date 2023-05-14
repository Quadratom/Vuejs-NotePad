<script setup>
import { ref } from "vue";

const showmodal = ref(false)
const notemodal = ref("")
const errormessage = ref("")
const addnote = ref([])


const getRanadomColor = () => {
return "hsl(" + Math.random() * 360 + ", 100%, 75%)";

}

const addnotebook = () => {
  if(notemodal.value.length < 10) {
    return errormessage.value = "Note should be 10 characters or more"
  }
  addnote.value.push({
    id: Math.floor(Math.random() * 1000000),
    item: notemodal.value,
    date: new Date,
    color: getRanadomColor()
  });
  showmodal.value = false;
  notemodal.value = ""
  errormessage.value = ""
}


</script>
<template>
 <main>
  <div v-if="showmodal" class="overlay">
    <div class="modal">
      <!-- {{ notemodal  }} -->
      <textarea v-model.trim="notemodal " name="name" id="name" cols="30" rows="10"></textarea>
      <p>{{ errormessage }}</p>
      <button @click="addnotebook">Add Note</button>
      <button class="close" @click="showmodal=false">close</button>
    </div>
  </div>
  <div class="container">
    <header>
      <h1>Notes</h1>
      <button @click="showmodal=true">+</button>
    </header>
    <div class="card-container">
      <div
       v-for="note in addnote"  
       :key="note.id" 
       class="card" 
       :style="{backgroundColor: note.color}">
        <p class="">{{ note.item }}</p>
        <p class="date">{{ note.date.toLocaleDateString("en-US") }}</p>
      </div>
    </div>
  
  </div>
  
 </main>
</template>


<style scoped>
main{
  height: 100vh;
  width: 100vw;
}

.container{
  max-width: 1000px;
  padding: 10px;
  margin: 0 auto;

}

header{
  display: flex;
  justify-content: space-between;
  align-items: center;
}

h1{
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 75px;
}

header button{
  border: none;
  padding: 10px;
  width: 50px;
  height: 50px;
  cursor: pointer;
  background-color: rgb(29, 23, 23);
  border-radius: 100%;
  color: white;
  font-size: 20px;
}
.card{
  width: 250px;
  height: 250px;
  background-color: blueviolet;
  padding: 10px;
  border-radius: 15px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 20px;
  margin-bottom: 20px;

}
.date{
  font-size: 12.5px;
  font-weight: bold;
}
.card-container{
  display: flex;
  flex-wrap: wrap;
}

.overlay{
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgb(0, 0, 0, 0.77);
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: center;
}
.modal{
  width: 750px;
  background-color: white;
  border-radius: 10px;
  padding: 30px;
  position: relative; 
  display: flex;
  flex-direction: column;
}
.modal button{
  padding: 10px 20px;
  font-size: 20px;
  width: 100%;
  background-color: rgb(64, 23, 102);
  border: none;
  color: white;
  cursor: pointer;
  margin-top: 15px;
}
.modal .close{
  background-color: rgb(151, 47, 47);
}
.modal p{
  color: rgb(151, 47, 47);
}

</style>
