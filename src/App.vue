<script>
import contactData from "./contacts.json";
export default {
  name: "App",
  components: {},
  data() {
    const contacts = contactData.slice(0, 5);
    return {
      contacts: contacts,
    };
  },
  computed: {},
};
</script>

<template>
  <h1>IronContacts</h1>
  <div>
    <table style="width: 100%">
      <thead>
        <tr>
          <th>Picture</th>
          <th>Name</th>
          <th>Popularity</th>
          <th>Won Oscar</th>
          <th>Won Emmy</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in contacts" :key="item.id">
          <td>
            <img :src="item.pictureUrl" alt="contact Image" />
          </td>
          <td>{{ item.name }}</td>
          <td>{{ item.popularity.toFixed(2) }}</td>
          <td >
            <img v-if="item.wonOscar" src="./assets/trophy.png" id="trophy" alt="" />
          </td>
          
          <td >
            <img v-if="item.wonEmmy" src="./assets/trophy.png" id="trophy" alt="" />
          </td>
         
        </tr>
      </tbody>
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
}
img {
  width: 100px;
  height: 120px;
}
#trophy{
  width: 80px;
  height: 80px;

}
</style>
