<template>
  <div class="wrapper-player">
    <!--Nếu activePlayer = 0 thì class active sẽ chạy(ở dưới có style cho active)-->
    <div class="player-panel" :class="{active: activePlayer == 0}">
        <div class="player-name">Player 1</div>
    <!--Điểm của PLAYER 1 nằm ở index 0 của mảng scorePlayers-->
        <div class="player-score">{{ scorePlayers[0] }}</div>
        <div class="player-current-box">
          <div class="player-current-label">Current</div>
          <div class="player-current-score">{{ activePlayer==0 ? currentScore : 0 }}</div>
        </div>
      </div>

      <div class="player-panel" :class="{active: activePlayer == 1}">
        <div class="player-name">Player 2</div>
        <div class="player-score">{{ scorePlayers[1] }}</div>
        <div class="player-current-box">
          <div class="player-current-label">Current</div>
          <div class="player-current-score">{{ activePlayer==1 ? currentScore : 0 }}</div>
        </div>
      </div>
  </div>
</template>

<script>
export default {
  name: 'players',
  props: {
    activePlayer:{type: Number, default: 0},
    currentScore: {type: Number, default: 0},
    scorePlayers: {type: Array, default: [0, 0]}
  },
  data () {
    return{

    }
  }
}
</script>

<style scoped>
.player-panel {
  width: 50%;
  float: left;
  height: 600px;
  padding: 100px;
  transition: all 0.3s ease;
  background-color: #fff;
}
.player-name {
  font-size: 40px;
  text-align: center;
  text-transform: uppercase;
  letter-spacing: 2px;
  font-weight: 100;
  margin-top: 20px;
  margin-bottom: 10px;
  position: relative;
}

.player-score {
  text-align: center;
  font-size: 80px;
  font-weight: 100;
  color: black;
  margin-bottom: 130px;
}

.active {
  background-color: #f7f7f7;
}
.active .player-name {
  font-weight: 300;
}

.active .player-name::after {
  content: "\2022";
  font-size: 47px;
  position: absolute;
  color: red;
  top: -7px;
  right: 10px;
}

.player-current-box {
  background-color: red;
  color: #fff;
  width: 40%;
  margin: 0 auto;
  padding: 12px;
  text-align: center;
}

.player-current-label {
  text-transform: uppercase;
  margin-bottom: 10px;
  font-size: 12px;
  color: #222;
}

.player-current-score {
  font-size: 30px;
}

.winner {
  background-color: #f7f7f7;
}
.winner .player-name {
  font-weight: 300;
  color: red;
}
</style>