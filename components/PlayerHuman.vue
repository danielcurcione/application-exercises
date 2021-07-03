<template>
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
</template>

<script>
export default {
  methods: {
    submit(e) {
      this.$parent.submit(e)
    }
  }
}
</script>