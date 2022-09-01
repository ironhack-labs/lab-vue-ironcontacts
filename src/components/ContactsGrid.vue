<template>
	<div class="contact-buttons">
		<button class="contact-button" :disabled="addRandomContactDisabled"
			:class="{ disabled: addRandomContactDisabled }" @click="addRandomContactToShowingContacts">Add Random
			Contact</button>
		<button class="contact-button" @click="sortByName">Sort by name</button>
		<button class="contact-button" @click="sortByPopularity">Sort by popularity</button>
	</div>
	<div class="grid">
		<div class="grid-heading"><b>Picture</b></div>
		<div class="grid-heading"><b>Name</b></div>
		<div class="grid-heading"><b>Popularity</b></div>
		<div class="grid-heading"><b>Won Oscar</b></div>
		<div class="grid-heading"><b>Won Emmy</b></div>
		<template class="grid-item" v-for="(contact, index) in sortedShowingContacts" :key="index"
			:v-if="showingContacts.length > 0">
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
const SortType = Object.freeze({ None: 0, Name: 1, Popularity: 2 });

export default {
	name: 'ContactsGrid',
	data() {
		return {
			limit: 5,
			showingContacts: [],
			remainingContacts: [],
			sortType: SortType.None,
		};
	},
	components: {

	},
	props: {
		contacts: [],

	},
	computed: {

		addRandomContactDisabled() {
			return this.remainingContacts.length === 0;
		},
		sortedShowingContacts() {
			if (this.sortType === SortType.Name) {
				return this.showingContacts.sort((a, b) => {
					return a.name.localeCompare(b.name);
				});
			} else if (this.sortType === SortType.Popularity) {
				return this.showingContacts.sort((a, b) => {
					return b.popularity - a.popularity;
				});
			} else {
				return this.showingContacts;
			}
		},
	},
	methods: {
		setInitialShowingContacts() {
			this.showingContacts = this.contacts.slice(0, this.limit);
			this.remainingContacts = this.contacts.slice(this.limit);
		},
		addRandomContactToShowingContacts() {
			if (this.remainingContacts.length > 0) {
				const remainingRandomContactIndex = Math.floor(Math.random() * this.remainingContacts.length);
				const randomContact = this.remainingContacts[remainingRandomContactIndex];
				// remove the random contact from the remaining contacts array
				this.remainingContacts.splice(remainingRandomContactIndex, 1);
				this.showingContacts.unshift(randomContact);
			}
		},
		sortByName() {
			this.sortType = SortType.Name;
		},
		sortByPopularity() {
			this.sortType = SortType.Popularity;
		}
	},
	mounted() {
		this.setInitialShowingContacts();
	}
}
</script>

<style>
.contact-buttons {
	display: flex;
	justify-content: space-between;
	align-items: center;
	width: 500px;
	margin: 0 auto;
	margin-bottom: 20px;
}

.contact-button {
	display: block;
	margin: 0 auto;
	width: 150px;
	background-color: #42adad;
	color: white;
	border: none;
	border-radius: 5px;
	height: 25px;
}

.contact-button.disabled {
	opacity: 0.5;
}

.grid {
	margin-top: 40px;
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
