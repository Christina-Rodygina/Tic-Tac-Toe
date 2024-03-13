<script>
export default {
  props: {
    player1: String,
    player2: String,
    player1_wins: Number,
    player2_wins: Number,
    timerPlayer1: Number,
    timerPlayer2: Number
  }
}
</script>

<template>
  <header class="ttt-head">
    <div class="container">
      <div class="ttt-head__row">
        <div class="player-info">
          <div class="info-1">
            <img src="/cross-svgrepo-com.svg" alt="Крестик">
            <div class="time-and-name">
              <span class="name">{{ player1 }}</span>
              <span class="timer" :style="{ color: timerPlayer1 <= 10 ? 'red' : 'white' }">
                {{timerPlayer1 === 60 ? ('01:00') : timerPlayer1 >= 10 ? (`00:${timerPlayer1}`) : (`00:0${timerPlayer1}`) }}
              </span>
            </div>
          </div>
          <div class="img-and-num">
            <div class="img-avatar">
              <img src="/11fcfbf6-558d-4336-95ea-077f1577272f.svg" alt="Аватар">
            </div>
            <span>{{ player1_wins }}</span>
          </div>
        </div>
        <div class="player-info-2">
          <div class="info-2">
            <img src="/circle-svgrepo-com.svg" alt="Нолик">
            <div class="time-and-name-2">
              <span class="name">{{ player2 }}</span>
              <span class="timer">
                {{ timerPlayer2 === 60 ? ('01:00') : (`00:${timerPlayer2}`) }}
              </span>
            </div>
          </div>
          <div class="img-and-num-2">
            <div class="img-avatar">
              <img src="/robot.svg" alt="Аватар">
            </div>
            <span>{{ player2_wins }}</span>
          </div>
        </div>
      </div>
    </div>
  </header>
</template>

<style scoped>

</style>