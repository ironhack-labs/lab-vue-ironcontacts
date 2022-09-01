<template>
	<div class="grid">
		<div class="grid-heading"><b>Picture</b></div>
		<div class="grid-heading"><b>Name</b></div>
		<div class="grid-heading"><b>Popularity</b></div>
		<div class="grid-heading"><b>Won Oscar</b></div>
		<div class="grid-heading"><b>Won Emmy</b></div>
		<template class="grid-item" v-for="(contact, index) in showingContacts" :key="index">
			<div class="contact-image">
				<img :src="contact.pictureUrl" alt="">
			</div>
			<div class="grid-text">{{ contact.name }}</div>
			<div class="grid-text">{{ contact.popularity.toFixed(2) }}</div>
			<div class="grid-text">
				<span v-if="contact.wonOscar">🏆</span>
			</div>
			<div class="grid-text"><span v-if="contact.wonEmmy">🏆</span></div>
		</template>
	</div>
</template>
<script>
export default {
	name: 'ContactsGrid',
	data() {
		return {
			limit: 5,
			showingContacts: []
		};
	},
	components: {

	},
	props: {
		contacts: [],
	},
	computed: {
	
	},
	methods: {
	},
	created() {
		this.showingContacts = this.contacts.slice(0, this.limit);
	}
}
</script>

<style>
.grid {
	display: grid;
	grid-template-columns: 100px 100px 100px 100px 100px;
	margin: auto;
	width: 500px;
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
