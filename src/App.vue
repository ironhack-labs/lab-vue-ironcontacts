<template>
	<h1>IronContacts</h1>
	<ContactsGrid :contacts="contacts"></ContactsGrid>
</template>

<script>
	import ContactsGrid from './components/ContactsGrid.vue';
	export default {
	name: 'App',
	components: {
		ContactsGrid,
	},
	data() {
		return {
			contacts: [],
		};
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
	created() {
		this.fetchContacts();
	}
}
</script>

<style>
	h1 {
		text-align: center;
	}
</style>
