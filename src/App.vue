<template>
	<div id="app">
		<div class="panel scores">
			<Transition 
				enter-active-class="animated animate__rubberBand"
				leave-active-class="animated animate__hinge" mode="out-in">
				<PanelComponent v-if="playerLife > 0"
					title =  'Jogador'
					:life = playerLife />
			</Transition>
			
			<Transition 
				enter-active-class="animated animate__rubberBand"
				leave-active-class="animated animate__hinge" mode="out-in">
				<PanelComponent v-if="monsterLife > 0"
					title =  'Monstro'
					:life = monsterLife />
			</Transition>
		</div>

		<VencedorComponents 
			:resultado = hasResult
			:life = monsterLife />

		<div class="panel buttons">
			<template v-if="running">
				<ButtonComponent :funcao = 'attack' classe="attack" nome="Ataque" />
				<ButtonComponent :funcao = 'attackSpecial' classe="special-attack" nome="Ataque Especial" />
				<ButtonComponent :funcao = 'healAndHurt' classe="heal" nome="Curar" />
				<ButtonComponent :funcao = "giveUp" classe="give-up" nome="Desistir" />
			</template>

			<template v-else >
				<ButtonComponent :funcao = 'startGame' classe="new_game" nome="Novo Jogo" />
			</template>

		</div>

	</div>
</template>

<script>

import PanelComponent from './components/PanelComponent.vue'
import ButtonComponent from './components/ButtonComponent.vue'
import VencedorComponents from './components/VencedorComponents.vue'

export default {
	name: 'App',
	components: {
		PanelComponent,
		ButtonComponent,
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
		giveUp() {
			this.running = false;
			this.playerLife = 100;
			this.monsterLife = 100;
		},
		attack() {
			this.hurt('playerLife', 7, 12, false)
			this.hurt('monsterLife', 5, 10, false)
		},
		attackSpecial() {
			this.hurt('playerLife', 7, 12, true)
			this.hurt('monsterLife', 5, 10, true)
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

</style>
