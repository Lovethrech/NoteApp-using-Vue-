<script setup>
import { ref } from 'vue';
const showModal = ref(false);
const newNote = ref("");
const errorMessage = ref("");
const notes = ref([]);

function getRandomColor() {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%";
}

const addNote = () => {
  if (newNote.value.length < 10) {
    return errorMessage.value = "Minimum note length is 10";
  }

  notes.value.push({
    id: Math.floor(Math.random() * 100000),
    text: newNote.value,
    date: new Date(),
    backgroundColor: getRandomColor()
  });
  showModal.value = false;
  newNote.value = "";
  errorMessage.value = "";
}
</script>

<template>
  <main>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <textarea v-model.trim="newNote" name="note" id="note" cols="30" rows="10"></textarea><br>
        <p v-if="errorMessage">{{ errorMessage }}</p>
        <button class="add" @click="addNote">Add Note</button>
        <button class="close" @click="showModal=false">Close</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>NoteApp</h1>
        <button @click="showModal=true">+</button>
      </header>
      <div class="card-container">
        <div v-for="note in notes" :key="note.id" class="card" :style="{backgroundColor:note.backgroundColor}">
          <p class="main-text">{{ note.text }}</p>
          <p class="date">{{ note.date.toLocaleDateString("en-US") }}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
main{
  width:100vw;
  height:100vh;
}
h1{
  font-weight:bold;
  letter-spacing: -2px;
}
main .container{
  margin:0;
  padding: 0;
}
main .container header{
  background-color: hsl(0, 1%, 55%);
  padding: 10px 20px;
  display:flex;
  flex-direction: row;
  justify-content: space-between;
  align-items:center;
  border-radius: 0 0 40px 40px;
}
main .container header button{
  background-color: hsl(0, 0%, 0%);
  color: hsl(0, 100%, 100%);
  padding:  10px 20px;
  border-radius: 100%;
  font-size:16px;
}
main .container header button:hover{
  background-color: hsl(0, 100%, 100%);
  color: hsl(0, 0%, 0%);
  border:2px solid hsl(0, 100%, 100%);
  transform:scale(0.9);
  transition: all 1s;
}
.card-container{
  margin-top:10px;
  display:flex;
  flex-wrap:wrap;
}
.card{
  width:225px;
  height: 225px;
  padding:20px;
  border-radius: 10px;
  display:flex;
  flex-direction: column;
  justify-content:space-between;
  margin: 0 20px 20px 0;
}
.date{
  font-size:small;
  font-weight:bold;
}

.overlay{
  position:absolute;
  width:100%;
  height:100%;
  background-color: hsla(0, 0%, 0%, 0.34);
  z-index: 10;
  display:flex;
  align-items: center;
  justify-content: center;
}
.overlay .modal{
  position:relative;
  display:flex;
  flex-direction:column;
  justify-content: space-between;
  width: 70%;
  background-color: hsl(0, 100%, 100%);
  padding: 10px;
  border-radius: 20px 20px 0 0;
}
.overlay .modal textarea{
  border-radius: 20px 20px 0 0;
  padding:20px;
  font-size: 24px;
}
.overlay .modal button.add{
  background-color: hsl(0, 0%, 0%);
  color:hsl(0, 100%, 100%);
  padding:10px;
  font-size:20px;
}
.overlay .modal button.add:hover, .overlay .modal button.close:hover{
  transition: all .42s;
  transform: scaleY(0.85);
}
.overlay .modal button.close{
  margin-top:10px;
  background-color: hsla(0, 92%, 48%, 0.43);
  color:hsl(0, 100%, 100%);
  border: 1px solid hsla(0, 92%, 48%, 0.43);
  padding:10px;
  font-size:20px;
}
.modal p{
  color:hsl(0, 100%, 50%);
  font:14px;
}

</style>
