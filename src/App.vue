<script>
import contactData from "./contacts.json";
export default {
  name: "App",
  components: {},
  data() {
    return {
      myArray: contactData,
      fivecontacts: [],
    };
  },
  //creamos la primera lista con los 5 primeros elementos del array de data
  created() {
    for (let i = 0; i < 5; i++) {
      this.fivecontacts.push(this.myArray.shift()); //en las primeras 5 iteraciones lanzadas con el metodo created añadimos 5 elementos del Data importado a 2 array: la primera que enseñaremos y la que contendra todos los elemetos que en adelante vayamos printando
    }
  },
  methods: {
    //elegimos un n º aleatorio del 5 al 1000
    getRandomInt(min, max) {
      const intMin = Math.ceil(min);
      const intMax = Math.floor(max);
      return Math.floor(Math.random() * (intMax - intMin) + intMin);
    },
    //usamos ese nº aleatorio como indice en el array para extraer un elemento
    getRandomElem() {
      if (this.myArray.length) {
        const myRandomPos = this.getRandomInt(0, this.myArray.length - 1);
        // console.log(myRandomPos);
        const myRandomElem = this.myArray[myRandomPos];
        const elemIsAvailableToShow = this.fivecontacts.findIndex(
          (elem) => elem === myRandomElem
        );
        //si está disponible, lo añadimos a la lista arrayToShow
        if (elemIsAvailableToShow === -1) {
          this.fivecontacts.push(myRandomElem);
          const elemToRemoveIndex = this.myArray.findIndex(
            (elem) => elem === myRandomElem
          );
          this.myArray.splice(elemToRemoveIndex, 1);
        }
      }
    },
    sortByName() {
      this.fivecontacts.sort((a, b) => (a.name > b.name ? 1 : -1));
    },
    sortByPopularity() {
      this.fivecontacts.sort((a, b) => (a.popularity > b.popularity ? 1 : -1));
    },
  },
};
</script>

<template>
  <h1>IronContacts</h1>
  <button @click="getRandomElem">Add Random Contact</button>
  <button @click="sortByName">Sort by Name</button>
  <button @click="sortByPopularity">Sort by Popularity</button>

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
      <tbody v-if="fivecontacts.length">
        <tr v-for="item in fivecontacts" :key="item.id">
          <td>
            <img :src="item.pictureUrl" alt="contact Image" />
          </td>
          <td>{{ item.name }}</td>
          <td>{{ item.popularity.toFixed(2) }}</td>
          <td>
            <img
              v-if="item.wonOscar"
              src="./assets/trophy.png"
              id="trophy"
              alt=""
            />
          </td>

          <td>
            <img
              v-if="item.wonEmmy"
              src="./assets/trophy.png"
              id="trophy"
              alt=""
            />
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
button {
  width: 30%;
  margin: 10px;
}
img {
  width: 100px;
  height: 120px;
}
#trophy {
  width: 80px;
  height: 80px;
}
</style>
