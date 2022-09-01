<template>
	<div>
		<ShowContact :contacts="getContact" />
	</div>
</template>

<script>
	import { computed } from "@vue/runtime-core";
	import contactsJson from "./contacts.json";
	import ShowContact from "./components/ShowContact.vue";

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
					};
				});
			},
		},
		components: { ShowContact },
	};
</script>

<style></style>
