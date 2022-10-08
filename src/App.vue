<script setup>
import contactsJson from './contacts.json';
import { ref } from 'vue'

const isNameAsc = ref(false);
const isPopAsc = ref(false);
const allContacts = ref(contactsJson);
const contacts = ref(contactsJson.slice(0,5));
console.log(contacts.value);

function selectRandomArtist(){
  let artist = allContacts.value[Math.floor(Math.random() * allContacts.value.length)];
  return artist;
}

function addRandomArtist(){
  let artist = selectRandomArtist();
  const found = contacts.value.some(element => element.name === artist.name); 
  console.log(found);
  console.log(contacts.value)
  if (!found){
    contacts.value.unshift(artist);
  } else {
    alert("The random contact selected was already in the list. Click again.")
  }
}

function sortByName(items){
  if (isNameAsc.value === false) {
    items.sort((a, b) => a.name.localeCompare(b.name));
    isNameAsc.value = true;
    console.log(items)
  } else {
    items.reverse();
    isNameAsc.value = false;
    console.log(items)
  }
}

function sortByPop(items){
  if (isPopAsc.value === false) {
    items.sort((a, b) => {
      if (a.popularity > b.popularity ) { return 1;}
      if (a.popularity  < b.popularity ) { return -1;}
      return 0;
    });
    isPopAsc.value = true;
  return items.value;
  } else {
    items.reverse();
    isPopAsc.value = false;
  }
}


const deleteContact = (index) => {
  allContacts.value.push(allContacts.value[index]);
  return contacts.value.splice(index, 1);
};


</script>

<template>
  <div>
    <h1>Iron Contacts</h1>
    <div class="buttonsRow">
      <button @click="addRandomArtist()">Add Random Contact</button>
      <button @click="sortByName(contacts)">Sort by Name</button>
      <button @click="sortByPop(contacts)">Sort by Popularity</button>
    </div>
    
    <table>
      <tr>
        <th>Picture</th>
        <th>Name</th>
        <th>Popularity</th>
        <th>Won an Oscar</th>
        <th>Won an Emmy</th>
        <th> Actions</th>
      </tr>
      <tr v-for="contact in contacts" :key="contact.id" id="artistRow">
        <td><img :src="contact.pictureUrl" alt="`${contact.name} picture`" /></td>
        <td>{{ contact.name }}</td>
        <td>{{ contact.popularity }}</td>
        <td><span v-if="contact.wonOscar">🏆</span></td>
        <td><span v-if="contact.wonEmmy">🏆</span></td>
        <td><Button @click="deleteContact()">Delete</Button></td>
      </tr>
    </table>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  justify-content: center;
}

th {
  padding: 0 20px;
}

table img {
  width: 100px;
}

button {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  border: none;
  padding: 10px 20px;
  background-color: #2c3e50;
  color: white;
  margin: 0px 5px 20px 5px;
}

button:hover {
  background-color: #727f8c;
  cursor: pointer;
}

</style>
