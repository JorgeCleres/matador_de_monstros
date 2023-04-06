<template>
	<div id="app">
		<div class="panel scores">
			<PanelComponent 
				title =  'Jogador'
				:life = playerLife />
			
			<PanelComponent 
				title =  'Monstro'
				:life = monsterLife />
		</div>

		<VencedorComponents 
			:resultado = hasResult
			:life = monsterLife />

		<div class="panel buttons">
			<template v-if="running">
				<button @click="attack" class="btn attack">Ataque</button>
				<button @click="attack(true)" class="btn special-attack">Ataque Especial</button>
				<button @click="healAndHurt" class="btn heal">Curar</button>
				<button @click="running = false" class="btn give-up">Desistir</button>
			</template>

			<button v-else @click="startGame" class="btn new-game">Novo Jogo</button>

		</div>

	</div>
</template>

<script>

import PanelComponent from './components/PanelComponent.vue'
//import ButtonComponent from './components/ButtonComponent.vue'
import VencedorComponents from './components/VencedorComponents.vue'

export default {
	name: 'App',
	components: {
		PanelComponent,
		//ButtonComponent,
		VencedorComponents
	},
	data() {
		return {
			running: false,
			playerLife: 100,
			monsterLife: 100
		}
	},
	computed: {
		hasResult() {
			return this.playerLife == 0 || this.monsterLife == 0
		}
	},

	methods: {
		startGame() {
			this.running = true;
			this.playerLife = 100;
			this.monsterLife = 100;
		},
		attack(special) {
			this.hurt('playerLife', 7, 12, special)
			this.hurt('monsterLife', 5, 10, special)
		},
		hurt(atr, min, max, special) {
			const plus = special ? 5 : 0
			const hurt = this.getRandom(min + plus, max - plus)
			// se o resultado de this - hurt for < que 0 pego o O se não for pego o valor de this - hurt
			this[atr] = Math.max(this[atr] - hurt, 0)
		},
		healAndHurt() {
			this.heal(10, 15)
			this.hurt('playerLife', 7, 12, false)
		},
		heal(min, max) {
			const heal = this.getRandom(min, max)
			// se o resultado de this + hurt for < que 100 pego o 10O se não for pego o valor de this - hurt
			this.playerLife = Math.min(this.playerLife + heal, 100)
		},
		getRandom(min, max) {
			const value = Math.random() * (max - min) + min
			return Math.round(value)
		}

	},

	watch: {
		hasResult(value) {
			if(value) this.running = false
		}
	}
}
</script>

<style>
	#app {
		display: flex;
		flex-direction: column;
	}


/** scores **/

	.scores {
		display: flex;
	}

	.score {
		flex: 1;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}

	.score h1 {
		font-weight: 300;;
		font-size: 1.6rem;
	}

	.life-bar {
		width:80%;
		height: 20px;
		border: 1px solid #AAA;
	}

	.life-bar .life {
		display: flex;
		justify-content: center;
		height: 100%;
		background-color: green;
	}

	.life-bar .life.danger {
		background-color: red;
	}

/** result */

	.result {
		display: flex;
		justify-content: center;
		font-size: 1.3rem;
		font-weight: 600;
	}

	.result .win {
		color: green
	}

	.result .lose {
		color: red
	}

	/** Buttons **/

	.buttons {
		display: flex;
		justify-content: center
	}

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
