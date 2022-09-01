<template>
  <div>
    <h1>Iron Contacts</h1>
    <table class="table">
      <thead>
        <td><b>Picture</b></td>
        <td><b>Name</b></td>
        <td><b>Popularity</b></td>
      </thead>
      <tbody v-for="fivecontact in fivecontacts" :key="fivecontact">
        <td><img :src="`${ fivecontact.pictureUrl }`" /></td>
        <td> {{ fivecontact.name }} </td>
        <td> {{ fivecontact.popularity }} </td>
      </tbody>
    </table>
  </div>
</template>

<script>
import contacts from "./contacts.json";

export default {
  name: 'App',
  data() {
    return {
      contacts: contacts,
      fivecontacts: [],
    }  
  },
  created() {
    let fiveContacts = contacts.slice(0, 5).push(fivecontacts);
    return {
      fiveContacts
    };
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
.table > tbody > td {
  padding-left: 150px;
}
img {
  height: 185px;
  width: 130px;
}
</style>
