<template>
  <div>

    <div :class="'game__section ' + classSection">
      <canvas id="confettiCanvas"></canvas>

      <PlayerHuman v-if="mode == 'humanVSmachine'"/>
      <PlayerComputer v-else-if="mode == 'machineVSmachine'" playerName="Macchina 1"/>
      <div>
        <h1 class="title has-text-white-ter countdown" v-show="countdown > -1">{{ countdown }}</h1>
        <h1 class="title has-text-white-ter countdown" v-show="countdown == -1">{{ textLoadingItem | toUpper }}</h1>
        <h2 class="is-2 game-results" v-show="buttonReset">{{ finalResults }}</h2>
        <h4 class="has-text-grey is-4 reset-button" v-show="buttonReset" @click="restart">Ricomincia</h4>
        <h4 class="has-text-grey is-4 reset-button" v-show="buttonReset" @click="changeMode">Cambia modalità</h4>
      </div>
      <PlayerComputer v-if="mode == 'humanVSmachine'" playerName="Avversario"/>
      <PlayerComputer v-else-if="mode == 'machineVSmachine'" playerName="Macchina 2"/>
    </div>

  </div>
</template>

<script>
import ConfettiGenerator from "confetti-js";

export default {
  name: 'GameBoard',
  props: ['mode'],
  data() {
    return {
      classSection: '',
      moveSelected: null,
      countdown: null,
      textLoadingItem: null,
      moves: ['rock', 'paper', 'scissor'],
      winMoves: [ ['rock', 'scissor'], ['paper', 'rock'], ['scissor', 'paper'] ],
      playerMove: null,
      machineMove: null,
      finalResults: null,
      buttonReset: false
    }
  },
  mounted() {
    if (this.mode == 'humanVSmachine') this.classSection = 'game__section__human'
    else if (this.mode == 'machineVSmachine') this.classSection = 'game__section__machine'
    else this.classSection = ''
  },
  methods: {
    /**
     * Sistemazione campo da gioco
     */
    restart(e) {
      this.buttonReset = false
      this.countdown = null
      this.selectItem(e)
    },
    changeMode(e) {
      this.buttonReset = false
      this.countdown = null
      this.$parent.menuItemSelected = null
    },

    /**
     * Scelta della modalità di gioco e inizio del countdown
     */
    selectItem(e) {
      if (this.moveSelected) {                      // cancellazione giocata precedente
        this.moveSelected.target.classList.remove('itemSelected')
        this.moveSelected = null
        this.playerMove = null                        
        this.machineMove = null
        this.buttonReset = false
      }

      this.$parent.menuItemSelected = e             // rimozione del menù

      document.getElementById('alertLoading').style.display = "block";
      const images = document.getElementsByClassName('game__section__player')
      images.forEach(element => {                   // animazioni scelta del computer
        element.style.display = 'block'
      });

      this.countdown = 4

      const countdownInterval = setInterval(() => {
        if (this.countdown < 1) {
          document.getElementById('alertLoading').style.display = "none"; // fine del countdown
          this.loadingWinner()                      // loading di vittoria
          clearInterval(countdownInterval)
          return
        }
        this.countdown -= 1;
      }, 1000);
    },

    /**
     * Selezione di una card da parte del player umano
     */
    submit(e) {
      if (this.moveSelected)                        // se la scelta è già stata fatta, funzione annullata: non si può cambiare mossa
        return

      this.moveSelected = e                         // salvataggio scelta del player umano
      this.playerMove = e.target.alt
      
      e.target.classList.add('itemSelected')        // evidenza della scelta selezionata
    },
    
    /**
     * Animazione prima della vittoria ('ROCK-PAPER-SCISSOR')
     */
    loadingWinner() {
      this.countdown = -1                           // rimozione elementi di gioco
      const images = document.getElementsByClassName('game__section__player')
      images.forEach(element => {
        element.style.display = 'none'
      });

      var index = 0
      this.textLoadingItem = this.moves[index]      // inizio dell'animazione

      const textCountdownInterval = setInterval(() => {
        if (this.textLoadingItem === 'scissor') {   // fine dell'animazione
          clearInterval(textCountdownInterval)      // estrazione del vincitore
          this.winnerCheck()
          return
        }

        index += 1
        this.textLoadingItem = this.moves[index]
      }, 700);
    },

    /**
     * Estrazione del vincitore
     */
    winnerCheck() {
      const equals = (a, b) => JSON.stringify(a) === JSON.stringify(b);
      const results = []
      this.buttonReset = true

      if (this.mode == 'machineVSmachine') {          // computer vs computer
        results.push(this.moves[Math.floor(Math.random() * 3)])
        results.push(this.moves[Math.floor(Math.random() * 3)])
      } else {                                        // umano vs computer
        results.push(this.playerMove)
        results.push(this.moves[Math.floor(Math.random() * 3)])
      }

      this.finalResults = results[0] + ' - ' + results[1]

      if (results[0] == results[1]) {                 // pareggio
        this.textLoadingItem = 'TIE'
        return
      } else {
        if (this.mode == 'machineVSmachine') {
          for (var i=0; i<this.winMoves.length; i++) {
            if (equals(results, this.winMoves[i])) {  // vincita macchina 1
              this.textLoadingItem = 'MACCHINA 1 WIN'
              return
            }
          }

          this.textLoadingItem = 'MACCHINA 2 WIN'     // vincita macchina 2
        } else {
          for (var i=0; i<this.winMoves.length; i++) {
            if (equals(results, this.winMoves[i])) {  // vincita del player umano
              this.setConfetti()
              this.textLoadingItem = 'YOU WIN'
              return
            }
          }

          this.textLoadingItem = 'YOU LOSE'           // vincita del computer
        }
      }
    },

    /**
     * Animazione di vittoria
     */
    setConfetti() {
      var confettiElement = document.getElementById('confettiCanvas');
      var confettiSettings = {
        target: confettiElement,
        max: 250,
        clock: 120,
        respawn: false,
        start_from_edge: true,
        rotate: true
      };
      var confetti = new ConfettiGenerator(confettiSettings);
      confettiElement.style.display = 'block'
      confetti.render();

      setTimeout(() => {
        confetti.clear()
        confettiElement.style.display = 'none'
      }, 2000)
    },
  },
  filters: {
    toUpper: function (value) {
      if (!value)return ''
      value = value.toString()
      return value.toUpperCase()
    }
  }
}
</script>