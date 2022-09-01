<template>
	<div>
		<table style="width: 80%; margin: 0 auto">
			<tr>
				<td>Picture</td>
				<td>Name</td>
				<td>Popularity</td>
				<td>Won Oscar</td>
				<td>Won Emy</td>
			</tr>
			<tr v-for="contact in contacts" :key="contact.id">
				<td>
					<img class="img-profile" :src="contact.picture" :alt="contact.name" />
				</td>
				<td>{{ contact.name }}</td>
				<td>{{ contact.popularity }}</td>
				<td v-show="contact.oscar">
					<img
						class="trofeo"
						src="https://cdn-icons-png.flaticon.com/512/3254/3254738.png"
					/>
				</td>
				<td v-show="contact.emy">
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
	export default {
		name: "ShowContact",
		props: {
			contacts: Array,
		},
	};
</script>

<style>
	.img-profile {
		width: 20%;
	}

	.trofeo {
		width: 50px;
	}
</style>
