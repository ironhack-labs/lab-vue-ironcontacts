<template>
  <div>
    <h1>Iron Contacts</h1>
    <button @click="getRandomElem">Add a Random Contact</button>
    <button @click="mostPopular">Sort by popularity</button>
    <button @click="alphabetic">Sort by name</button>
    <table class="table">
      <thead>
        <td><b>Picture</b></td>
        <td><b>Name</b></td>
        <td><b>Popularity</b></td>
        <td><b>Won an Oscar</b></td>
        <td><b>Won an Emmy</b></td>
        <td><b>Actions</b></td>
      </thead>
      <tbody>
        <tr v-for="contact in fiveContacts" :key="contact.id">
          <td><img :src="`${ contact.pictureUrl }`" class="actor-img"/></td>
          <td> {{ contact.name }} </td>
          <td> {{ contact.popularity }} </td>
          <td><img v-if=" contact.wonOscar " src="../src/assets/icons8-trophy-48.png" alt="trophy"></td>
          <td><img v-if=" contact.wonEmmy " src="../src/assets/icons8-trophy-48.png" alt="trophy"></td>
          <td><button @click="deleteElem(contact.id)">Delete</button></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import contactsData from "./contacts.json";

export default {
  name: 'App',
  data() {
    return {
      contacts: contactsData,
      fiveContacts: [],
    }
  },
  created() {
    for (let i = 0; i < 5; i++) {
      this.fiveContacts.push(this.contacts.shift())
    }
  },
  methods: {
    getRandomInt(min, max) {
      min = Math.ceil(min);
      max = Math.floor(max);
      return Math.floor(Math.random() * (max - min) + min);
    },
    getRandomElem() {
      if (this.contacts.length) {
        const randomPos = this.getRandomInt(0, this.contacts.length - 1);
        const randomElem = this.contacts[randomPos];
        const elemToShow = this.fiveContacts.findIndex(elem => elem === randomElem);

        if (elemToShow === -1) {
          this.fiveContacts.push(randomElem);
          const elemToRemoveIndex = this.contacts.findIndex(elem => elem === randomElem);
          this.contacts.splice(elemToRemoveIndex, 1);
        }
      }
    },
    mostPopular() {
      this.fiveContacts.sort((a,b) => a.popularity < b.popularity ? 1 : -1);
    },
    alphabetic() {
      this.fiveContacts.sort((a,b) => a.name > b.name ? 1 : -1);
    },
    deleteElem(contactId) {
      const contactToDelete = this.fiveContacts.findIndex(elem => elem.id === contactId);
      if (contactToDelete !== -1) {
        this.contacts.push(this.fiveContacts.splice(contactToDelete, 1)[0]);
      }
    }
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.table > thead > td {
  padding-left: 60px;
}
.table > tbody > tr > td {
  padding-left: 30px;
}
.actor-img {
  height: 185px;
  width: 130px;
}
</style>
