<template>
  <div class="janela">
    <div class="main-container">
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
    <button v-on:click="teste()">
      clique aqui
    </button>
    <div class="main-container">
      <div class="options" id="stone">
        <img src="@/assets/pedra.png" class="icon">
      </div>
      <div class="options" id="scissors">
        <img src="@/assets/tesoura.png" class="icon">
      </div>
      <div class="options" id="paper">
        <img src="@/assets/papel.png" class="icon">
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      player: '',
      computer: '',
      results: ''
    }
  },
  methods: {
    getComputerChoice() {
      const pcChoice = ['stone', 'scissors', 'paper']
      let randomIndex = Math.floor(Math.random() * 3)
      this.computer = pcChoice[randomIndex]
      console.log('pc', this.computer)
    },
    getPlayerChoice() {
      this.player = event.currentTarget.id
      console.log('player', this.player)
      this.getComputerChoice()
      this.checkWinner()
    },
    checkWinner() {
      if ((this.player == 'paper' && this.computer == 'stone') || (this.player == 'stone' && this.computer == 'paper') || (this.player == 'scissors' && this.computer == 'paper')) {
        this.results = 'Jogador Ganhou'
      } else if (this.player ==  this.computer) {
        this.results = 'Empate'
      } else {
        this.results = 'Computador Ganhou'
      }
      alert(this.results)
    }
  }
}
</script>
<style>
.janela {
  border: 1px solid red;
  justify-content: space-between;
  display: flex;
  gap: 10vw;
}

.main-container {
  position: relative;
  width: 30vw;
  height: 30vw;
  border-radius: 50%;
  border: 1px solid black;
  display: flex;
  align-items: center;
  justify-content: center;
}

.options {
  height: 10vw;
  width: 10vw;
  border-radius: 50%;
  border: 1px solid red;
  position: absolute;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: black;
}

.options:hover {
  cursor: pointer;
  background-color: aqua;

}

.icon {
  height: 17vh;
  z-index: 1;
}

#stone {
  top: 0;
}

#paper {
  right: 0;
  margin-bottom: -5vw;
}

#scissors {
  left: 0;
  margin-bottom: -5vw;
}
</style>