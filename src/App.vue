<template>
  <div id="app">
    <h1 class="title">Iron Contacts</h1>
    <table class ="contactstable">
      <tr>
        <th>Picture</th>
        <th>Name</th>
        <th>Popularity</th>
      </tr>
      <tr v-for="contact in fivecontacts" :key="contact.id">
        <td><img class="picture" :src="contact.pictureUrl" /></td>
        <td>
          <p>{{ contact.name }}</p>
        </td>
        <td>
          <p>{{ contact.popularity }}</p>
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
    let fivecontacts = contacts.slice(0, 5);
    return {
      fivecontacts,
    };
  },
};
</script>

<style>

.picture {
  width:100px;
}
.contactstable {
  text-align: center;
}
#app {
  width:100%;
  display: flex;
  flex-flow: column;
  align-items: center;
}
</style>