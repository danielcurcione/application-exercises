<template>
  <div class="game__section__player game__section__player_machine">
    <h1 class="title has-text-white-ter">{{ playerName }}</h1>
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
</template>

<script>
export default {
  props: ['playerName']
}
</script>