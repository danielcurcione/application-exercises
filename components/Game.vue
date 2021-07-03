<template>
  <div class="game">
    <div class="game__menu" v-show="!menuItemSelected">
      <h1 class="title">Seleziona una modalità</h1>

      <ul class="game__menu__items">
        <li class="game__menu__item"> <span @click="selectHuman">Uomo VS Macchina</span> </li>
        <li class="game__menu__item"> <span @click="selectMachine">Macchina VS Macchina</span> </li>
      </ul>
    </div>

    <GameBoard mode="humanVSmachine" ref="gameBoardHuman" v-show="mode == 'humanVSmachine'"/>
    <GameBoard mode="machineVSmachine" ref="gameBoardMachine" v-show="mode == 'machineVSmachine'"/>

  </div>
</template>


<script>
import GameBoard from './GameBoard';

export default {
  data() {
    return {
      menuItemSelected: null,
      mode: '',
    }
  },
  methods: {
    /**
     * Creazione del campo da gioco in base alla modalità scelta
     */
    selectHuman(e) {
      this.mode = 'humanVSmachine'
      this.$refs.gameBoardHuman.selectItem(e)
    },
    selectMachine(e) {
      this.mode = 'machineVSmachine'
      this.$refs.gameBoardMachine.selectItem(e)
    },
  },
  components: {
    GameBoard
  },
}
</script>