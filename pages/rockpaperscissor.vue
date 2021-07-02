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
          <div class="game__section__player game__section__player_human">
            <h1 class="title has-text-white-ter">Tu</h1>
            <div class="images">
              <div class="image">
                <img src="../assets/images/rock.png" @click="submit">
              </div>
              <div class="image">
                <img src="../assets/images/paper.png" @click="submit">
              </div>
              <div class="image">
                <img src="../assets/images/scissor.png" @click="submit">
              </div>
            </div>
          </div>
          <div>
            <h1 class="title has-text-white-ter countdown">{{ countdown }} </h1>
          </div>
          <div class="game__section__player game__section__player_machine">
            <h1 class="title has-text-white-ter">Avversario</h1>
            <div class="images">
              <div class="image">
                <img src="../assets/images/rock.png" @click="submit">
              </div>
              <div class="image">
                <img src="../assets/images/paper.png" @click="submit">
              </div>
              <div class="image">
                <img src="../assets/images/scissor.png" @click="submit">
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
export default {
  data() {
    return {
      menuItemSelected: null,
      imageSelected: null,
      modeHuman: false,
      modeMachine: false,
      countdown: null
    }
  },
  methods: {
    submit(e) {
      this.imageSelected = e.target.currentSrc
      e.target.classList.add('itemSelected')
    },

    selectHuman(e) {
      this.selectItem(e)
      this.modeHuman = true
      this.modeMachine = false
    },

    selectMachine(e) {
      this.selectItem(e)
      this.modeHuman = false
      this.modeMachine = true
    },

    selectItem(e) {
      // rimuovi eventuale item selezionato precedentemente
      if (this.menuItemSelected != null)
        this.menuItemSelected.target.classList.remove('active')
      
      // aggiungi il nuovo item selezionato
      this.menuItemSelected = e
      e.target.classList.add('active')
      
      debugger
      document.getElementById('alertLoading').style.display = "block";
      this.startCountDown()
    },

    startCountDown() {
      if (this.countdown > 0)
        return

      this.countdown = 5

      const countdownInterval = setInterval(() => {
        if (this.countdown < 1) {
          document.getElementById('alertLoading').style.display = "none";
          clearInterval(countdownInterval)
          return
        }

        this.countdown -= 1;
      }, 1000);
    }
  }
}
</script>