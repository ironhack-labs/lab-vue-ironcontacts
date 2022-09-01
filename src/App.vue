<template>
  <div>
    <h1>Iron Contacts</h1>
    <!-- <button @click=addRandom()>Add a Random Contact</button> -->
    <table class="table">
      <thead>
        <td><b>Picture</b></td>
        <td><b>Name</b></td>
        <td><b>Popularity</b></td>
        <td><b>Won an Oscar</b></td>
        <td><b>Won an Emmy</b></td>
      </thead>
      <tbody>
        <tr v-for="contact in contacts" :key="contact">
          <td><img :src="`${ contact.pictureUrl }`" /></td>
          <td> {{ contact.name }} </td>
          <td> {{ contact.popularity }} </td>
          <td><img v-if=" contact.wonOscar " src="../src/assets/trophy-solid-24.png" alt="trophy"></td>
          <td><img v-if=" contact.wonEmmy " src="../src/assets/trophy-solid-24.png" alt="trophy"></td>
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
  padding-left: 130px;
}
/* .table > tbody > tr {
  width: 90%;
} */
.table > tbody > tr > td {
  padding-left: 130px;
}
img {
  height: 185px;
  width: 130px;
}
</style>
