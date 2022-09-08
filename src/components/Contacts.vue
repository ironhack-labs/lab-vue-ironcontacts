<template>
    <div class="container" v-if="contacts.length">
        <button v-on:click="randomize">Add random contact</button>
        <h1>IronContacts</h1>
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
                </tr>
            </table>
        </div>
    </div>
    <div class="contact" v-for="contact in filteredContacts" :key="contact">
        <router-link to="/">
            <div class="contacts">
                <table style="width: 1000px">
                    <tr class="tabla">
                        <td><img :src="contact.pictureUrl" /></td>
                        <td>
                            <p>{{ contact.name }}</p>
                        </td>
                        <td>
                            <p>{{ contact.popularity }}</p>
                        </td>
                        <td v-if="contact.wonOscar">
                            <p>🏆</p>
                        </td>
                        <td v-else>
                            <p> </p>
                        </td>
                        <td v-if="contact.wonEmmy">
                            <p>🏆</p>
                        </td>
                        <td v-else>
                            <p> </p>
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
        }
    }
};
</script>

<style>
.tabla {
    display: flex;
    justify-content: space-around;
}

th {
    margin-left: 50px;
}

.contacts {
    display: flex;
    flex-direction: column;
    margin-left: 20px;
}

p,
h1 {
    color: black;
}

img {
    width: 120px;
}
</style>
