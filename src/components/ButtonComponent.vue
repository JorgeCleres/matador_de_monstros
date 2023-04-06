<template>
    <button :class="classe" class="btn attack">{{ nome }}</button>
</template>

<script>
export default {
    props: ['nome', 'classe'],
}
</script>

<style>

	.btn {
		padding: 5px 10px;
		margin: 0px 10px;
		border-radius: 5px;
		text-transform: uppercase;
		font-size: 1.1rem;
		color: white;
		border: 0px solid white
	}

	.new-game {
		background-color: blue;
	}
	.attack {
		background-color: red;
	}
	.special-attack {
		background-color: yellow;
		color: black
	}
	.heal {
		background-color: green;
	}
	.give-up {
		background-color: grey;
	}

</style>