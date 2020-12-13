<template>
	<div id="app">
        <div class="wrapper clearfix">

            <players 
                v-bind:activePlayer="activePlayer"
                v-bind:currentScore="currentScore"
                v-bind:scorePlayers="scorePlayers"
            />

            <controls
                v-bind:isPlaying="isPlaying"
                v-on:handleNewGame="handleNewGame"
                v-on:handleRollDice="handleRollDice"
            />
            
            <dices 
                v-bind:dices="dices"
            />
            
            <popup-rule 
                v-on:handleConfirm="handleConfirm"
                v-bind:isOpenPopup="isOpenPopup"
            />
        </div>
	</div>
</template>

<script>
import Controls from './components/Controls.vue';
import Dices from './components/Dices.vue';
import Players from './components/Players.vue';
import popupRule from './components/popupRule.vue';
import swal from 'sweetalert';
export default {
  name: "app",
  data() {
    return {
      scorePlayers: [0, 0], //điểm tổng của PLAYER: index 0 là điểm tổng PLAYER 1, index 1 là điểm tổng PLAYER 2
      activePlayer: 0, //Nếu 0 là PLAYER 1 đang chơi, nếu khác 0 thì PLAYER 2 đang chơi
      currentScore: 0, //Nếu PLAYER 1 đang chơi thì currentScore = 0 sẽ gán cho PLAYER 2 và ngược lại
      isPlaying: false, //Có đang chơi hay không? (false: không, true: có)
      isOpenPopup: false, //Popup luật chơi có đang mở hay không? (false: không, true: có)
      dices: [5,6], //trạng thái 2 mặt xúc xắc
    };
  },
  components: {
    Players,
    Controls,
    Dices,
    popupRule,
  },
  methods: {
    handleNewGame(){ //khi ấn "New Game"
      this.isOpenPopup = true; //popup (luật chơi) hiện
    },
    handleConfirm(){  //khi ấn "đã hiểu"
      this.isPlaying = true;      //trạng thái đang chơi dc bật
      this.isOpenPopup = false;   //tắt popup(luật chơi)
      this.activePlayer = 0;      //PLAYER 1 được active
      this.scorePlayers = [0,0];  //điểm tổng của người chơi dc set về 0
      this.currentScore = 0;   //điểm mặt xúc xắc set về 0
      this.dices = [1,1];   // 2 mặt xúc xắc set về 1
    },
    nextPlayer(){
      this.activePlayer = this.activePlayer === 0 ? 1:0; //PLAYER đang chơi có phải PLAYER 1 không? phải thì đổi thành PLAYER 2, không thì PLAYER 1
      this.currentScore = 0;
    },
    handleRollDice(){ //khi ấn Roll Dice
      if(this.isPlaying == true){   //nếu trạng thái đang chơi dc bật, đồng nghĩa với đã bấm "New Game" và "Đã hiểu"
        var dice1 = Math.ceil(Math.random()*6); //radom làm tròn lên từ 0-6
        var dice2 = Math.ceil(Math.random()*6);
        this.dices = [dice1, dice2]; //gán giá trị 2 mặt xúc xắc bằng 2 biến được radom ở trên
        this.nextPlayer(); //đổi lượt chơi cho PLAYER sau khi quay xong 1 lần
        if(dice1 == 1 || dice2==1 ) //nếu 1 trong 2 xúc xắc quay vào 1
        {
          setTimeout(function(){
          //thông báo cho người chơi đã quay trúng ô 1 sau 350ms (để giá trị currentScore được set về 0 trước khi chạy alert)
          swal('Bạn đã quay trúng ô 1 mất rùi :<');
          },350)
          //current PLAYER đó = 0
          this.currentScore = 0;
        }
        else{
          //điểm tính ở currentScore
          this.currentScore = dice1 + dice2;
        }
        this.scorePlayers[this.activePlayer] += this.currentScore;
      }
      else{
        swal('Nhấn vào New Game để bắt đầu'); //nếu PLAYER chưa nhấn vào "New Game" thì Roll Dice không hoạt động, PLAYER sẽ nhận dc lời nhắc
      }
    },
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.clearfix::after {
  content: "";
  display: table;
  clear: both;
}

body {
  background-image: linear-gradient(
      rgba(62, 20, 20, 0.4),
      rgba(62, 20, 20, 0.4)
    ),
    url("/public/assets/back.jpg");
  background-size: cover;
  background-position: center;
  font-family: Lato;
  font-weight: 300;
  position: relative;
  height: 100vh;
  color: #555;
}

.wrapper {
  width: 1000px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: #fff;
  box-shadow: 0px 10px 50px rgba(0, 0, 0, 0.3);
  overflow: hidden;
}
</style>
