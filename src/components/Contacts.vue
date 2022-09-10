<template>
    <div class="container" v-if="contacts.length">

        <h1 style="font-size: 50px;">IronContacts</h1>
        <button class="button" v-on:click="randomize">Add random contact</button>
        <button class="button" v-on:click="popSort">Sort by popularity</button>
        <button class="button" v-on:click="nameSort">Sort by name</button>
        <div class="contacts">
            <table style="width: 1000px">
                <tr class="tabla">
                    <th>
                        <h1>Picture</h1>
                    </th>
                    <th>
                        <h1>Name</h1>
                    </th>
                    <th>
                        <h1>Popularity</h1>
                    </th>
                    <th>
                        <h1>Won Oscar</h1>
                    </th>
                    <th>
                        <h1>Won Emmy</h1>
                    </th>
                    <th>
                        <h1>Actions</h1>
                    </th>
                </tr>
            </table>
        </div>
    </div>
    <div class="contact" v-for="(contact, index) in filteredContacts" :key="contact">
        <router-link style="text-decoration: none;" to="/">
            <div class="contacts">
                <table style="width: 1000px">
                    <tr class="tabla">
                        <td><img :src="contact.pictureUrl" /></td>
                        <td>
                            <p>{{ contact.name }}</p>
                        </td>
                        <td>
                            <p>{{ (contact.popularity).toFixed(2) }}</p>
                        </td>
                        <td v-if="contact.wonOscar">
                            <p>🏆</p>
                        </td>
                        <td v-else>
                            <p> </p>
                        </td>
                        <td v-if="contact.wonEmmy">
                            <p>⭐</p>
                        </td>
                        <td v-else>
                            <p> </p>
                        </td>
                        <td>
                            <button class="button" v-on:click="idDelete(index)">Delete</button>
                        </td>
                    </tr>
                </table>
            </div>
        </router-link>
    </div>
</template>

<script>
export default {
    data() {
        return {
            contacts: [],
            filteredContacts: [],
        };
    },
    async created() {
        const res = await fetch('./src/contacts.json')
        const data = await res.json()
        this.contacts = data
        this.filteredContacts = this.contacts.slice(0, 5);
    },
    methods: {
        randomize: function () {
            this.filteredContacts.push(this.contacts[Math.floor(Math.random() * this.contacts.length)]);
        },
        popSort: function () {
            this.filteredContacts.sort((a, b) => b.popularity - a.popularity);
        },
        nameSort: function () {
            this.filteredContacts.sort((a, b) => {
                if (a.name > b.name) return 1;
                else return -1;
            })
        },
        idDelete: function (index) {
            this.filteredContacts.splice(index, 1);
        }
    }
};
</script>

<style>
.contacts {
    width: 100%;
    display: flex;
    align-items: center;
    flex-direction: column;
}

.tabla {
    display: flex;
    justify-content: space-around;
}

th {
    width: 200px;
}

td {
    width: 200px;
    align-self: center;
}

p,
h1 {
    color: black;
}

p {
    font-size: 25px;
}

img {
    width: 100px;
}

.button {
    font-size: 20px;
    margin: 10px;
}
</style>
