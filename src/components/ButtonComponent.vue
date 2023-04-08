<template>
    <button @click="funcao" :class="classe" class="btn">{{ nome }}</button>
</template>

<script>
export default {
    //props: ['nome', 'classe'],
	props: {
		funcao: Function,
		nome: {
			type: String,
			default: 'Botão',
			required: true
		},
		classe: {
			type: String,
			default: ' ',
			required: true
		}
	}
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

	.new_game {
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