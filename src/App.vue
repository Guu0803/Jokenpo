<template>
  <div class="janela">
    <div class="score-container">
      Placar
      <div>
        <div class="score">
          {{ playerScore }}
        </div>
        -
        <div class="score">
          {{ computerScore }}
        </div>
      </div>
    </div>
    <div>
      <div class="main-container">
        <div class="player-winner" :style="showWinner('Jogador Ganhou')">
          Vencedor
        </div>
        <div class="oponent">
          Jogador
        </div>
        <div class="choices-container">
          <div class="options" id="stone" v-on:click="getPlayerChoice()">
            <img src="@/assets/pedra.png" class="icon">
          </div>
          <div class="options" id="scissors" v-on:click="getPlayerChoice()">
            <img src="@/assets/tesoura.png" class="icon">
          </div>
          <div class="options" id="paper" v-on:click="getPlayerChoice()">
            <img src="@/assets/papel.png" class="icon">
          </div>
        </div>
      </div>
      <div class="vs-container">
        <div class="letter" id="letter-v">V</div>
        <div class="letter" id="letter-s">S</div>
      </div>
      <div class="main-container">
        <div class="pc-winner" :style="showWinner('Computador Ganhou')">
          Vencedor
        </div>
        <div class="oponent">
          Computador
        </div>
        <div class="choices-container">
          <div class="pc-options" id="pc-stone" :style="showComputerChoice('stone')">
            <img src="@/assets/pedra.png" class="icon">
          </div>
          <div class="pc-options" id="pc-scissors" :style="showComputerChoice('scissors')">
            <img src="@/assets/tesoura.png" class="icon">
          </div>
          <div class="pc-options" id="pc-paper" :style="showComputerChoice('paper')">
            <img src="@/assets/papel.png" class="icon">
          </div>
        </div>
      </div>
    </div>
    <div class="a-tie" v-if="this.winner == 'Empate'">
      Empatou!
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      player: '',
      computer: '',
      winner: '',
      playerScore: 0,
      computerScore: 0
    }
  },
  methods: {
    getComputerChoice() {
      this.computer = undefined
        setTimeout(() => {
          const pcChoice = ['stone', 'scissors', 'paper']
          let randomIndex = Math.floor(Math.random() * 3)
          this.computer = pcChoice[randomIndex]
        }, 50);
    },
     getPlayerChoice() {
      this.getComputerChoice()
      this.player = event.currentTarget.id
      setTimeout(() => {
      this.checkWinner()
      }, 100);
    },
    checkWinner() {
      if (this.player == this.computer) {
        this.winner = 'Empate'
        this.showATie()
      } else if ((this.player == 'stone' && this.computer == 'scissors') || (this.player == 'paper' && this.computer == 'stone') || (this.player == 'scissors' && this.computer == 'paper')) {
        this.winner = 'Jogador Ganhou'
        this.playerScore++
      } else {
        this.computerScore++
        this.winner = 'Computador Ganhou'
      }
    },
    showComputerChoice(option) {
      if (option == this.computer) {
        return 'animation: myAnim 2s ease 0s 1 normal forwards;'
      } else {
        return 'animation: unset;'
      }
    },
    showWinner(winner) {
      if (this.playerScore == 5 || this.computerScore == 5) {
        if (winner == this.winner) {
          return 'display:block;'
        }
      }
    },
    showATie() {
      setTimeout(() => {
        this.winner = ''
      }, 2000);
    }

  },
  watch: {
    playerScore() {
      if (this.playerScore == 5) {
        setTimeout(() => {
          this.playerScore = 0
          this.computerScore = 0
        }, 3000);
      }
    },
    computerScore() {
      if (this.computerScore == 5) {
        setTimeout(() => {
          this.computerScore = 0
          this.playerScore = 0
        }, 3000);
      }
    }
  }
}
</script>
<style>
body {
  margin: 0;
}

.janela {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  position: relative;
  box-sizing: border-box;
  padding: 0 3vw;
  width: 100vw;
  height: 100vh;
  background-image: url('@/assets/wallpaper.jpg');
  background-size: cover;
  background-position: center;
}

.janela>div {
  display: flex;
  align-items: center;
  justify-content: center;
}

.score-container {
  font-size: 7vh;
  flex-direction: column;
  gap: 3vh;
  font-family: 'Press Start 2P';
  -webkit-text-stroke-width: 2px;
  -webkit-text-stroke-color: white;
  position: absolute;
  top: 3vh;
  border: 3px solid white;
  padding: 2vh;
  box-sizing: border-box;
  border-radius: 15px;
}

.score-container>div {
  display: flex;
  gap: 2vw;
  align-items: center;
}

.score {
  font-size: 10vh;
}

.main-container {
  position: relative;
  height: fit-content;
  padding: 1vw;
  gap: 3vh;
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.choices-container {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1vh;

}

.oponent,
.pc-winner,
.player-winner {
  color: black;
  font-family: 'Press Start 2P';
  font-size: 7vh;
  -webkit-text-stroke-width: 2px;
  -webkit-text-stroke-color: white;
}

.pc-winner,
.player-winner {
  animation: winner 2s ease 0s infinite normal forwards;
  display: none;
  position: absolute;
  top: -5vw;
}

.vs-container {
  position: relative;
  width: 20vw;
  height: 20vw;
  display: flex;
  align-items: center;
  justify-content: center;
}

.letter {
  font-family: 'Press Start 2P';
  font-size: 18vh;
  color: black;
  z-index: 3;
  position: absolute;
  -webkit-text-stroke-width: 3px;
  -webkit-text-stroke-color: white;
  transform: rotate(10deg);
}

#letter-v {
  left: 3vw;
  top: 4vw;
}

#letter-s {
  margin: 7vw 0 0 4vw;
}

.a-tie {
  color: black;
  font-family: 'Press Start 2P';
  font-size: 7vh;
  -webkit-text-stroke-width: 2px;
  -webkit-text-stroke-color: white;
  position: absolute;
  bottom: 12vh;
  animation: winner 2s ease 0s 1 normal forwards;
}

.options,
.pc-options {
  height: 10vw;
  width: 10vw;
  border-radius: 15px;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 3px 3px 10px black;
  border: 3px solid white;
}

.options:hover {
  cursor: pointer;
  background-color: rgba(255, 255, 255, 0.384);
}

.icon {
  height: 20vh;
  z-index: 1;
}

@keyframes myAnim {

  0%,
  50%,
  100% {
    background-color: rgba(255, 25, 25, 0);
  }

  25%,
  75% {
    background-color: rgba(252, 252, 252, 0.521);
  }
}

@keyframes winner {

  0%,
  50%,
  100% {
    scale: 1;
  }

  25%,
  75% {
    scale: 1.1;
  }
}
</style>