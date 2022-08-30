<template>
  
    <h1>Iron Contacts</h1>
    
    <button type="button" @click="addRandomContact">Add Random Contact</button>
    <button type="button" @click="sortByPopularity">Sort By Popularity</button>
    <button type="button" @click="sortByName">Sort By Name</button>
    <table>
    <tr class="top-row">
      <th>
        <h2>Picture</h2>
      </th>
      <th>
        <h2>Name</h2>
      </th>
      <th>
        <h2>Popularity</h2>
      </th>
      <th>
        <h2>Won Oscar</h2>
      </th>
      <th>
        <h2>Won Emmy</h2>
      </th>
       <th>
        <h2>Actions</h2>
      </th>
    </tr>
    <tr v-for="contact in contactsDataComputed" :key="contact.id">
      <td><img :src="contact.pictureUrl" class="contact-image" /></td>
      <td>{{ contact.name }}</td>
      <td>{{ contact.popularity }}</td>
      <td> <p v-if="contact.wonOscar">🏆</p></td>
      <td> <p v-if="contact.wonEmmy">🏆 </p></td>
      <td><button type="button" @click="deleteContact(contact)">Delete</button></td>
    
    </tr>
  </table>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.contact-image {
  height: 150px;
  width: auto;
}
button{
 margin: 10px;
}
table{
  width: 100%;
  row-gap: 5px;
  column-gap: 5px;
  border: 2px solid grey;
  border-collapse: collapse;
}
tr{
  border: 1px solid grey;
}
td {
  border: 1px solid grey;
}

.top-row{
  border-bottom: 2px solid grey;
 
}
th{
  border-left: 2px solid grey;
  color: white; 
  background-color: grey;
}
</style>

<script>
import contacts from "./contacts.json";
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import HelloWorld from "./components/HelloWorld.vue";

export default {
  data() {
    return {
      contactsData: contacts,
      contactListSize: 5,
      byPopularity: false,
      byName: false,
    };
  },
  computed: {
    contactsDataComputed() {
      if (this.sortByPopularity){
       

        }
      else if(this.sortByName){
        this.sortByPopularity=false;
      }
      return this.contactsData.slice(0, this.contactListSize);
    },
  },
  methods: {
    addRandomContact() {
      
      let randomContact=[];
      let position=0;
      if (this.contactListSize < this.contactsData.length) {
        while (position < this.contactListSize) {
          position=Math.floor(Math.random() * (this.contactsData.length-this.contactListSize))+this.contactListSize
          randomContact = this.contactsData[position];
         
        }
        const oldContact= this.contactsData[this.contactListSize];
        this.contactsData[this.contactListSize]=randomContact;
        this.contactsData[position]=oldContact;
        this.contactListSize++;
      }
      else {
        console.log("Ya se ha mostrado toda la lista");
      }
    },
    sortByPopularity(){
       this.contactsData.sort((a,b) => b.popularity - a.popularity);
       this.byName=false;
       this.byPopularity=true;
    },
    sortByName(){
      this.contactsData.sort((a,b) => a.name.localeCompare(b.name));
      this.byName=true;
      this.byPopularity=false;
    },
    deleteContact(contact){
      this.contactsData.splice(this.contactsData.indexOf(contact),1);
      this.contactListSize--;
    }   
  },
};
</script>
