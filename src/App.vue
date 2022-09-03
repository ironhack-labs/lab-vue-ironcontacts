<template>
  <div id="app">
    <h1 class="title">Iron Contacts</h1>
    <article>
      <button class="contactbuttons" @click="addRandom">
        Add Random Contact
      </button>
      <button class="contactbuttons" @click="mostPopular">
        Sort by Popularity
      </button>
      <button class="contactbuttons" @click="alphabeticalOrder">
        Sort by Name
      </button>
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
      <tr v-for="contact in fiveContacts" :key="contact.id">
        <td><img class="picture" :src="contact.pictureUrl" /></td>
        <td>
          <p>{{ contact.name }}</p>
        </td>
        <td>
          <p>{{ contact.popularity }}</p>
        </td>
        <td>
          <img
            alt="trophy"
            class="trophy"
            v-if="contact.wonOscar"
            src="./assets/Oscar.png"
          />
        </td>
        <td>
          <img
            alt="trophy"
            class="trophy"
            v-if="contact.wonEmmy"
            src="./assets/Emmy.png"
          />
        </td>
        <td>
          <button class="contactbuttons" @click="removeContact(contact.id)">
            Delete
          </button>
        </td>
      </tr>
    </table>
  </div>
</template>


<script>
import contacts from "./contacts.json";

export default {
  name: "App",
  data() {
    return {
      contacts: contacts,
      fiveContacts: [],
    };
  },
  created() {
    for (let i = 0; i < 5; i++) {
      this.fiveContacts.push(this.contacts.shift());
    }
  },

  methods: {
    getRandom(min, max) {
      min = Math.ceil(min);
      max = Math.floor(max);
      return Math.floor(Math.random() * (max - min) + min);
    },
    addRandom() {
      if (this.contacts.length) {
        const myRandomPos = this.getRandom(0, this.contacts.length - 1);
        const myRandomElem = this.contacts[myRandomPos];
        const elemAvailable = this.fiveContacts.findIndex(
          (elem) => elem === myRandomElem
        );

        if (elemAvailable === -1) {
          this.fiveContacts.unshift(myRandomElem);
          const contacToRemove = this.contacts.findIndex(
            (elem) => elem === myRandomElem
          );
          this.contacts.splice(contacToRemove, 1);
        }
      }
    },
    mostPopular() {
      this.fiveContacts.sort((a, b) => (a.popularity < b.popularity ? 1 : -1));
    },
    alphabeticalOrder() {
      this.fiveContacts.sort((a, b) => (a.name > b.name ? 1 : -1));
    },
    removeContact(contactId) {
      const contactIndex = this.fiveContacts.findIndex(
        (elem) => elem.id === contactId
      );
      if (contactIndex !== -1) {
        this.contacts.push(this.fiveContacts.splice(contactIndex, 1)[0]);
      }
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
.contactbuttons {
  background-color: bisque;
}
#app {
  width: 100%;
  display: flex;
  flex-flow: column;
  align-items: center;
}
.trophy {
  width: 30px;
}
</style>