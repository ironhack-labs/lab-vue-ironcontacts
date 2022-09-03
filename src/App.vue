<template>
	<div>
		<Buttons :range="range" />
		<ShowContact :contacts="selectedContacts" />
	</div>
</template>

<script>
	import contactsJson from "./contacts.json";
	import ShowContact from "./components/ShowContact.vue";
	import Buttons from "./components/Buttons.vue";

	export default {
		name: "App",
		data() {
			return {
				selectedContacts: [],
				contacts: contactsJson,
				range: contactsJson.length,
			};
		},

		methods: {
			getContact() {
				let index = 0;
				const formatContacts = contactsJson.map((contact) => {
					const contacts = [{}];
					contacts.ID = contact.ID;
					contacts.name = contact.name;
					contacts.picture = contact.pictureUrl;
					contacts.popularity = contact.popularity.toFixed([2]);
					contacts.oscar = contact.wonOscar;
					contacts.emmy = contact.wonEmmy;
					index++;
					contacts.index = index;
					return contacts;
				});
				this.selectedContacts = formatContacts.slice(0, 5);
				return formatContacts;
			},
		},
		components: { ShowContact, Buttons },
	};
</script>

<style></style>
