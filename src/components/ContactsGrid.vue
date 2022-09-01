<template>
	<div class="grid">
		<div class="grid-heading"><b>Picture</b></div>
		<div class="grid-heading"><b>Name</b></div>
		<div class="grid-heading"><b>Popularity</b></div>
		<template class="grid-item" v-for="(contact, index) in contacts" :key="index">
			<div class="contact-image">
				<img :src="contact.pictureUrl" alt="">
			</div>
			<div class="grid-text">{{ contact.name }}</div>
			<div class="grid-text">{{ contact.popularity.toFixed(2) }}</div>
		</template>
	</div>
</template>
<script>
export default {
	name: 'ContactsGrid',
	components: {

	},
	props: {
		contacts: [],
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
.grid {
	display: grid;
	grid-template-columns: 200px 200px 200px;
	margin: auto;
    width: 600px;
}
.grid-heading {
	margin-bottom: 20px;
	text-align: center;
}
.grid-text {
	text-align: center;
	padding: 30px 0;
}

.contact-image img {
	width: 50px;
	height: 90px;
	background-color: #eee;
	object-fit: cover;
	margin: auto;
	display: block;
	margin-bottom: 20px;
}
</style>
