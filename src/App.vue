<template>
	<div>
		<Buttons />
		<ShowContact :contacts="getContact" />
	</div>
</template>

<script>
	import { computed } from "@vue/runtime-core";
	import contactsJson from "./contacts.json";
	import ShowContact from "./components/ShowContact.vue";
	import Buttons from "./components/Buttons.vue";

	export default {
		name: "App",
		data() {
			return {
				contacts: contactsJson,
			};
		},
		computed: {
			getContact() {
				return this.contacts.map((contact) => {
					return {
						name: contact.name,
						picture: contact.pictureUrl,
						popularity: contact.popularity.toFixed([2]),
						oscar: contact.wonOscar,
						emy: contact.wonEmmy,
					};
				});
			},
		},
		components: { ShowContact, Buttons },
	};
</script>

<style></style>
