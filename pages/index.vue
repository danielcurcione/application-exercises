<template>
  <div class="container is-max-desktop">
    
    <div class="section homepage">
      <nav class="breadcrumb has-succeeds-separator" aria-label="breadcrumbs">
        <ul>
          <li>
            <nuxt-link to="/"> <a class="has-text-white-ter">Home</a> </nuxt-link>
          </li>
        </ul>
      </nav>

      <h5 class="title has-text-grey is-5 mb-1">Candidatura</h5>
      <h1 class="title has-text-white-ter is-1">Daniel Curcione</h1>

      <div class="apps">
        <div class="block apps__block">
          <div class="block mb-1 is-flex is-align-items-center is-flex-direction-row">
            <span class="mr-2"> 📄 </span>
            <nuxt-link to="/foobar">
              <h3 class="title has-text-white-ter is-3">FooBar ↗</h3>
            </nuxt-link>
          </div>
          <div class="block has-text-grey-light pl-2 pr-2 pb-2">
            Scrivi un piccolo programma che stampi ogni numero da 1 a 100 su una nuova riga.  Per ogni multiplo di 3, stampa “Foo” invece del numero.  Per ogni multiplo di 5, stampa “Bar” invece del numero.  Per ogni numero multiplo di 3 e 5 insieme, stampa “FooBar” invece del numero.
          </div>
        </div>
        <div class="block apps__block">
          <div class="block mb-1 is-flex is-align-items-center is-flex-direction-row">
            <span class="mr-2"> ✌🏻 </span>
            <nuxt-link to="/">
              <h3 class="title has-text-white-ter is-3">Rock Paper Scissors ↗</h3>
            </nuxt-link> 
          </div>
          <div class="block has-text-grey-light pl-2 pr-2 pb-2">
            Sono un assiduo giocatore, per questo voglio giocare a “carta forbice e sasso”. Posso giocare Umano vs Computer? Posso giocare Computer vs Computer? Posso giocare una nuova partita conclusa quella precedente?
          </div>
        </div>
      </div>
    </div>
    
  </div>
</template>