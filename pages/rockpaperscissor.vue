<template>
  <div class="container is-max-desktop">
    
    <div class="section homepage">
      <nav class="breadcrumb" aria-label="breadcrumbs">
        <ul>
          <li>
            <nuxt-link to="/" style="margin: 0; padding: 0"> <a class="has-text-grey">Home</a> </nuxt-link>
          </li>
          <li>
            <nuxt-link to="/" style="margin: 0; padding: 0"> <a class="has-text-white-ter">Rock Paper Scissor</a> </nuxt-link>
          </li>
        </ul>
      </nav>

      <h5 class="title has-text-grey is-5 mb-1">Esercitazione 2</h5>
      <h1 class="title has-text-white-ter is-1">Rock Paper Scissor ✌🏼✋🏼✊🏼 </h1>

      <div class="game">
        <div class="game__menu">
          <h1 class="title">Seleziona una modalità</h1>

          <ul class="game__menu__items">
            <li class="game__menu__item"> <span @click="selectHuman" key="uomo">Uomo VS Macchina</span> </li>
            <li class="game__menu__item"> <span @click="selectMachine" key="macchina">Macchina VS Macchina</span> </li>
          </ul>
        </div>

        <div class="game__section game__section__human" v-show="modeHuman">
          <canvas id="confettiCanvas"></canvas>

          <div class="game__section__player game__section__player_human">
            <h1 class="title has-text-white-ter">Tu</h1>
            <div class="images">
              <div class="image">
                <img src="../assets/images/rock.png" alt="rock" @click="submit">
              </div>
              <div class="image">
                <img src="../assets/images/paper.png" alt="paper" @click="submit">
              </div>
              <div class="image">
                <img src="../assets/images/scissor.png" alt="scissor" @click="submit">
              </div>
            </div>
          </div>
          <div>
            <h1 class="title has-text-white-ter countdown" v-show="countdown > -1">{{ countdown }}</h1>
            <h1 class="title has-text-white-ter countdown" v-show="countdown == -1">{{ textLoadingItem | toUpper }}</h1>
            <h2 class="has-text-grey-light is-2 game-results" v-show="buttonReset">{{ playerMove }} - {{ machineMove }}</h2>
            <h4 class="has-text-grey is-4 reset-button" v-show="buttonReset == true" @click="selectHuman">Ricomincia</h4>
          </div>
          <div class="game__section__player game__section__player_machine">
            <h1 class="title has-text-white-ter">Avversario</h1>
            <div class="images">
              <div class="image">
                <img src="../assets/images/rock.png">
              </div>
              <div class="image">
                <img src="../assets/images/paper.png">
              </div>
              <div class="image">
                <img src="../assets/images/scissor.png">
              </div>
              <div id="alertLoading" class="alert">
                <p>Sta scegliendo...</p>
              </div>
            </div>
            
          </div>
        </div>

        <div class="game__section game__section__machine" v-show="modeMachine">
          Machine
        </div>
      </div>

    </div>
    
  </div>
</template>

<script>
import ConfettiGenerator from "confetti-js";

export default {
  data() {
    return {
      menuItemSelected: null,
      moveSelected: null,
      imageSelected: null,
      modeHuman: false,
      modeMachine: false,
      countdown: null,
      textLoadingItem: null,
      moves: ['rock', 'paper', 'scissor'],
      winMoves: [
        ['rock', 'scissor'],
        ['paper', 'rock'],
        ['scissor', 'paper']
      ],
      playerMove: null,
      machineMove: null,
      buttonReset: false
    }
  },
  methods: {
    submit(e) {
      if (this.moveSelected)
        return

      this.playerMove = e.target.alt
      this.machineMove = this.moves[Math.floor(Math.random() * 3)]
      this.moveSelected = e
      this.imageSelected = e.target.currentSrc

      if (!e.target.classList.toString().includes('itemSelected'))
        e.target.classList.add('itemSelected')
    },

    selectHuman(e) {
      this.selectItem(e)
      this.modeHuman = true
      this.modeMachine = false
      this.buttonReset = false
    },

    selectMachine(e) {
      this.selectItem(e)
      this.modeHuman = false
      this.modeMachine = true
    },

    selectItem(e) {
      if (this.moveSelected)
        this.moveSelected.target.classList.remove('itemSelected')

      this.moveSelected = null

      // rimuovi eventuale item selezionato precedentemente
      if (this.menuItemSelected != null)
        this.menuItemSelected.target.classList.remove('active')
      
      // aggiungi il nuovo item selezionato
      this.menuItemSelected = e
      e.target.classList.add('active')
      
      document.getElementById('alertLoading').style.display = "block";
      const images = document.getElementsByClassName('game__section__player')
      images.forEach(element => {
        element.style.display = 'block'
      });

      this.startCountDown()
    },

    startCountDown() {
      if (this.countdown > 0)
        return

      this.countdown = 4

      const countdownInterval = setInterval(() => {
        if (this.countdown < 1) {
          document.getElementById('alertLoading').style.display = "none";
          this.winGameCheck()
          clearInterval(countdownInterval)
          return
        }

        this.countdown -= 1;
      }, 1000);
    },

    winGameCheck() {
      this.countdown = -1
      const images = document.getElementsByClassName('game__section__player')

      images.forEach(element => {
        element.style.display = 'none'
      });

      var index = 0
      this.textLoadingItem = this.moves[index]

      const textCountdownInterval = setInterval(() => {
        if (this.textLoadingItem === 'scissor') {
          clearInterval(textCountdownInterval)
          this.movesCheck()
          return
        }

        index += 1
        this.textLoadingItem = this.moves[index]
      }, 750);
    },

    movesCheck() {
      const equals = (a, b) => JSON.stringify(a) === JSON.stringify(b);
      var results = [this.playerMove, this.machineMove]

      this.buttonReset = true
      if (this.playerMove == this.machineMove) {
        this.textLoadingItem = 'TIE'
        return
      } else {
        for (var i=0; i<this.winMoves.length; i++) {
          if (equals(results, this.winMoves[i])) {
            this.setConfetti()
            this.textLoadingItem = 'YOU WIN'
            return
          }
        }
      }

      this.textLoadingItem = 'YOU LOSE'
      return
    },

    setConfetti() {
      var confettiElement = document.getElementById('confettiCanvas');
      confettiElement.style.display = 'block'
      var confettiSettings = {
        target: confettiElement,
        max: 200,
        clock: 80,
        respawn: false,
        start_from_edge: true,
        rotate: true
      };
      var confetti = new ConfettiGenerator(confettiSettings);
      confetti.render();

      setTimeout(() => {
        confetti.clear()
        confettiElement.style.display = 'none'
      }, 2000)
    },
  },
  filters: {
    toUpper: function (value) {
      if (!value) return ''

      value = value.toString()
      return value.toUpperCase()
    }
  }
}
</script>