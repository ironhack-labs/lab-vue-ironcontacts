<template>
	<h1>IronContacts</h1>
	<ContactsGrid :contacts="contacts" v-if="contacts.length > 0"></ContactsGrid>
</template>

<script>
import ContactsGrid from './components/ContactsGrid.vue';
export default {
	name: 'App',
	components: {
		ContactsGrid,
	},
	data() {
		return { contacts: [] }
	},
	computed: {

	},
	methods: {
		async fetchContacts() {
			const response = await fetch('/contacts.json');
			const data = await response.json();
			this.contacts = data;
		},
	},
	mounted() {
		this.fetchContacts();
	}
}
</script>

<style>
 * {
	font-family: 'Lato', sans-serif;
}

h1 {
	text-align: center;
}
</style>
