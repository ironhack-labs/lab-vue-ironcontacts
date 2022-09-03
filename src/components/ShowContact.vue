<template>
	<div>
		<div class="btn-zone">
			<button v-on:click="activateFunction">Add random actor</button>
			<button v-on:click="sortPopularity">Sort Contact by Popularity</button>
			<button v-on:click="sortName">Sort Contact by Name</button>
		</div>
		<table class="table">
			<tr class="title">
				<td class="picture">Picture</td>
				<td>Name</td>
				<td>Popularity</td>
				<td>Won Oscar</td>
				<td>Won Emy</td>
			</tr>
			<tr v-for="contact in selectedContacts" :key="contact.id">
				<td class="img-space">
					<img
						class="img-profile"
						:src="contact.pictureUrl"
						:alt="contact.name"
					/>
				</td>
				<td>{{ contact.name }}</td>
				<td>{{ contact.popularity.toFixed([2]) }}</td>
				<td v-show="contact.wonOscar">
					<img
						class="trofeo"
						src="https://cdn-icons-png.flaticon.com/512/3254/3254738.png"
					/>
				</td>
				<td v-show="contact.wonEmmy">
					<img
						class="trofeo"
						src="https://cdn-icons-png.flaticon.com/512/3254/3254738.png"
					/>
				</td>
			</tr>
		</table>
	</div>
</template>

<script>
	import contactsJson from "../contacts.json";

	export default {
		name: "ShowContact",
		data() {
			return {
				selectedContacts: [],
				contacts: contactsJson,
			};
		},

		created() {
			this.selectedContacts = this.contacts.slice(0, 5);
			this.contacts.splice(0, 5);
		},

		methods: {
			addRandom(min, max) {
				console.log(Math.floor(Math.random() * (max - min + 1) + min));
				return Math.floor(Math.random() * (max - min + 1) + min);
			},
			activateFunction() {
				console.log(this.contacts.length);
				if (this.contacts.length) {
					const randomNumber = this.addRandom(0, this.contacts.length - 1);
					const randomContact = this.contacts[randomNumber];
					this.selectedContacts.push(randomContact);
					this.contacts.splice(randomNumber, 1);
				}
			},
			sortPopularity() {
				this.selectedContacts = this.selectedContacts.sort(
					(a, b) => b.popularity - a.popularity
				);
			},
			sortName() {
				this.selectedContacts = this.selectedContacts.sort((a, b) =>
					a.name > b.name ? 1 : -1
				);
			},
		},
	};
</script>

<style>
	body {
		font-family: Arial, Helvetica, sans-serif;
	}

	.img-profile {
		width: 70px;
	}

	.trofeo {
		width: 50px;
	}

	.btn-zone {
		width: 70%;
		margin: 0 auto;
		display: flex;
		justify-content: space-between;
		align-items: center;
		flex-wrap: nowrap;
		flex-direction: row;
		padding-top: 4%;
		padding-bottom: 4%;
	}

	.table {
		width: 70%;
		margin: 0 auto;
		text-align: center;
	}

	.title {
		font-weight: bold;
		line-height: 3em;
		font-size: 1.2em;
	}

	.picture {
		width: min-content;
	}

	.img-space {
		width: 20%;
	}
</style>
