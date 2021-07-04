<template>
  <div class="container is-max-desktop">
    
    <div class="section homepage">
      <Header title="Daniel Curcione" subtitle="Candidatura" link="home"/>

      <a href="https://github.com/danielcurcione/application-exercises" class="button is-dark is-small mt-3">GitHub</a>
      <a href="https://www.linkedin.com/in/danielcurcione/" class="button is-dark is-small mt-3">LinkedIn</a>

      <div class="apps">
        <template v-for="app in apps">
          <AppContainer :icon="app.icon" :title="app.title" :link="app.link" :description="app.description" :key="app.title"/>
        </template>
      </div>
    </div>
    
  </div>
</template>

<script>
export default {
  data() {
    return {
      apps: [{
        icon: '📄',
        title: 'FooBar',
        link: '/foobar',
        description: 'Scrivi un piccolo programma che stampi ogni numero da 1 a 100 su una nuova riga. Per ogni multiplo di 3, stampa “Foo” invece del numero. Per ogni multiplo di 5, stampa “Bar” invece del numero. Per ogni numero multiplo di 3 e 5 insieme, stampa “FooBar” invece del numero.'
      }, {
        icon: '✌🏻',
        title: 'Rock Paper Scissor',
        link: '/rockpaperscissor',
        description: 'Sono un assiduo giocatore, per questo voglio giocare a “carta forbice e sasso”. Posso giocare Umano vs Computer? Posso giocare Computer vs Computer? Posso giocare una nuova partita conclusa quella precedente?'
      }]
    }
  }
}
</script>