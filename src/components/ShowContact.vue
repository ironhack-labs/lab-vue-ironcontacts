<template>
	<div>
		<table style="width: 100%">
			<tr>
				<td>Picture</td>
				<td>Name</td>
				<td>Popularity</td>
			</tr>
			<tr v-for="n in 5" :key="contacts[n].id">
				<td>
					<img
						class="img-profile"
						:src="contacts[n].picture"
						:alt="contacts[n].name"
					/>
				</td>
				<td>{{ contacts[n].name }}</td>
				<td>{{ contacts[n].popularity }}</td>
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
</style>
