<template>
  <div>
    <h1>Iron Contacts</h1>
    <table class="table">
      <thead>
        <td><b>Picture</b></td>
        <td><b>Name</b></td>
        <td><b>Popularity</b></td>
      </thead>
      <tbody>
        <tr v-for="contact in contacts" :key="contact">
          <td><img :src="`${ contact.pictureUrl }`" /></td>
          <td> {{ contact.name }} </td>
          <td> {{ contact.popularity }} </td>
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
    let contacts = contactsData.slice(0, 5);
    return {
      contacts: contacts,
    }  
  },
  // methods: {
  //   addRandom() {
  //     let randomContactList = contacts.splice(5, contacts.lenght-1);
  //     this.fiveContacts.unshift(randomContactList[0]);
  //   },
  //   mostPopular() {
  //     let popular = this.fiveContacts.sort((a,b) => a.popularity < b.popularity);
  //     return popular;
  //   },
  // },
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
  padding-left: 160px;
}
.table > tbody > tr > td {
  padding-left: 150px;
}
img {
  height: 185px;
  width: 130px;
}
</style>
