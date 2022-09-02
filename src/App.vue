<script>
import contactData from "./contacts.json";
export default {
  name: "App",
  components: {},
  data() {
    const myArray = JSON.parse(JSON.stringify(contactData));
    let fivecontacts = contactData.slice(0, 5);
    const myArrayToShow = [];
    return {     
      fivecontacts,
      myArray,
      myArrayToShow,
    };
  },
  // computed: {},
  methods: { //      NOFUNCIONA
    //creamos la primera lista con los 5 primeros elementos del array de data
    created() {
      const fivecontacts = [];
      for (i = 0; i < 5; i++) {
        myArrayToShow.push(myArray.unshift()); //en las primeras 5 iteraciones lanzadas con el metodo created añadimos 5 elementos del Data importado a 2 array: la primera que enseñaremos y la que contendra todos los elemetos que en adelante vayamos printando
      }
    },
    //elegimos un n º aleatorio del 5 al 1000
    getRandomInt() {
      min = Math.ceil(min);
      max = Math.floor(max);
      return Mathgi.floor(Math.random() * (max - min) + min);
    }, //Esto devuelve un decimal!!!
   
    //usamos ese nº aleatorio como indice en el array para extraer un elemento
    getRandomElem() {
      if (this.myArray.length) {
        const myRandomPos = getRandomInt(0, this.myArray.length - 1);
        const myRandomElem = this.myArray[myRandomPos];
        const elemIsAvailableToShow = myArrayToShow.findIndex(
          (elem) => elem === myRandomElem
        );
        //si está disponible, lo añadimos a la lista arrayToShow
        if (elemIsAvailableToShow === -1) {
          myArrayToShow.push(myRandomElem);
          const elemToRemoveIndex = myArray.findIndex(
            (elem) => elem === myRandomElem
          );
          myArray.splice(elemToRemoveIndex, 1);
        }
      }
    },
  },
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
  <button @click="getRandomElem">Add Random Contact</button>
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
#trophy {
  width: 80px;
  height: 80px;
}
</style>
