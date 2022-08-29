<template>
  <div id="app">
    <h1 class="title">Iron Contacts</h1>
    <article class="contactbuttons">
      <button @click="addrandom">Add Random Contact</button>
      <button @click="mostpopular">Sort by Popularity</button>
      <button @click="alphabeticalorder">Sort by Name</button>
    </article>
    <br />
    <table class="contactstable">
      <tr>
        <th>Picture</th>
        <th>Name</th>
        <th>Popularity</th>
        <th>Won Oscar</th>
        <th>Won Emmy</th>
        <th>Actions</th>
      </tr>
      <tr v-for="contact in fivecontacts" :key="contact.id">
        <td><img class="picture" :src="contact.pictureUrl" /></td>
        <td>
          <p>{{ contact.name }}</p>
        </td>
        <td>
          <p>{{ contact.popularity }}</p>
        </td>
        <td v-if="contact.wonOscar">Yes!!</td>
        <td v-else></td>
        <td v-if="contact.wonEmmy">Yes!!</td>
        <td v-else></td>
        <td><button @click="removecontact(contact)">Delete</button></td>
      </tr>
    </table>
  </div>
</template>


<script>
import contacts from "./contacts.json";

export default {
  name: "App",
  data() {
    let fivecontacts = contacts.slice(5, 10);
    return {
      fivecontacts,
    };
  },
  methods: {
    addrandom() {
      let randomcontactlist = contacts.splice(6, 5);
      this.fivecontacts.unshift(randomcontactlist[0]);
    },
    mostpopular() {
      let popular = this.fivecontacts.sort((a, b) => {
        if (a.popularity > b.popularity) {
          return -1;
        } else if (a.popularity < b.popularity) {
          return 1;
        } else {
          return 0;
        }
        return { popular };
      });
    },
    alphabeticalorder() {
      let orderbyname = this.fivecontacts.sort((a, b) => {
        if (a.name < b.name) {
          return -1;
        } else if (a.name > b.name) {
          return 1;
        } else {
          return 0;
        }
        return { orderbyname };
      });
    },
    removecontact(contact) {
      this.fivecontacts = this.fivecontacts.filter((t) => t !== contact);
    },
  },
};
</script>

<style>
.picture {
  width: 100px;
}
.contactstable {
  text-align: center;
}
#app {
  width: 100%;
  display: flex;
  flex-flow: column;
  align-items: center;
}
</style>