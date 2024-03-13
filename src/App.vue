<script>
import "./styles/reset.css";
import "./styles/App.css";
import Header from "./components/header.vue";
import Footer from "@/components/footer.vue";
import Game from "@/components/game.vue";

export default {
  components: {Game, Footer, Header},
  data() {
    const xg = "/cross-svgrepo-com.svg";
    const og = "/circle-svgrepo-com.svg";
    return {
      player1: '',
      player2: '',
      player1_wins: 0, //num
      player2_wins: 0, //num
      x: xg, //src
      o: og, //src
      currentStep: 'x', //symbol
      timePlayer1: 30,
      timePlayer2: 30,
      isActivePlayer1: false,
      isActivePlayer2: false,
      change: false,
      winner: '', //name
      tttList: [null, null, null, null, null, null, null, null, null], //array
      isHovered: [false, false, false, false, false, false, false, false, false] //array
    }
  },
  methods: {
    startTimer() {
      const win_block = document.querySelector(".win-block")
      const table = document.querySelector(".ttt__body-tbl")
      const btn = document.querySelector(".ttt-footer button")
      if (this.currentStep === 'x') {
        this.isActivePlayer1 = true;
        if (this.timePlayer1 > 0) {
          this.timePlayer1--;
          setTimeout(this.startTimer, 1000);
        } else {
          this.stopTimer()
          this.winner = this.player2
          this.updatePlayerWins(this.player2)
          win_block.classList.add("open")
          if (!table.classList.contains("non-clickable-block")) {
            table.classList.add("non-clickable-block")
            btn.classList.remove("non-clickable-block")
          }
        }
      } else if (this.currentStep === 'o') {
        this.isActivePlayer2 = true;
        if (this.timePlayer2 > 0) {
          this.timePlayer2--;
          setTimeout(this.startTimer, 1000);
        } else {
          this.stopTimer()
          this.winner = this.player1
          this.updatePlayerWins(this.player1)
          win_block.classList.add("open")
          if (!table.classList.contains("non-clickable-block")) {
            table.classList.add("non-clickable-block")
            btn.classList.remove("non-clickable-block")
          }
        }
      } else {
        this.isActivePlayer2 = false;
        this.isActivePlayer1 = false;
        if (!table.classList.contains("non-clickable-block")) {
          table.classList.add("non-clickable-block")
          btn.classList.remove("non-clickable-block")
        }
      }
    },
    stopTimer() {
      if (this.currentStep === 'x') {
        this.isActivePlayer1 = false;
      } else if (this.currentStep === 'o') {
        this.isActivePlayer2 = false;
      } else {
        this.isActivePlayer1 = false;
        this.isActivePlayer2 = false;
      }
    },
    selectCell(index) {
      if (this.currentStep === 'x') {
        this.tttList[index] = this.x;
        this.isHovered[index] = false;
        this.changePlayer('x')
      } else {
        this.tttList[index] = this.o;
        this.isHovered[index] = false;
        this.changePlayer('o')
      }
      this.$refs.game.checkingWin();
    },
    changePlayer(icon) {
      if (icon === 'x') {
        this.currentStep = 'o';
      } else {
        this.currentStep = 'x';
      }
    },
    // changeFocus(index) {
    //   if (!this.tttList[index]) {
    //     this.isHovered[index] = true;
    //   }
    // },
    // resetFocus(index) {
    //   this.isHovered[index] = false;
    // },
    // checkingWin() {
    //   const win_block = document.querySelector(".win-block")
    //   const text = document.querySelector('.win-block h2')
    //   const table = document.querySelector(".ttt__body-tbl")
    //   const btn = document.querySelector(".ttt-footer button")
    //   if (this.tttList[0] === this.tttList[1] && this.tttList[1] === this.tttList[2] && this.tttList[0] !== null) {
    //     win_block.classList.add("open");
    //     if (!table.classList.contains("non-clickable-block")) {
    //       table.classList.add("non-clickable-block")
    //       btn.classList.remove("non-clickable-block")
    //     }
    //     this.winner = this.tttList[0] === this.x ? this.player1 : this.player2;
    //     if (this.tttList[0] === this.x) {
    //       this.player1_wins++
    //     } else {
    //       this.player2_wins++
    //     }
    //   } else if (this.tttList[0] === this.tttList[4] && this.tttList[4] === this.tttList[8] && this.tttList[0] !== null) {
    //     win_block.classList.add("open");
    //     if (!table.classList.contains("non-clickable-block")) {
    //       table.classList.add("non-clickable-block")
    //     }
    //     this.winner = this.tttList[0] === this.x ? this.player1 : this.player2;
    //     if (this.tttList[0] === this.x) {
    //       this.player1_wins++
    //     } else {
    //       this.player2_wins++
    //     }
    //   } else if (this.tttList[0] === this.tttList[3] && this.tttList[3] === this.tttList[6] && this.tttList[0] !== null) {
    //     win_block.classList.add("open");
    //     if (!table.classList.contains("non-clickable-block")) {
    //       table.classList.add("non-clickable-block")
    //       btn.classList.remove("non-clickable-block")
    //     }
    //     this.winner = this.tttList[0] === this.x ? this.player1 : this.player2;
    //     if (this.tttList[0] === this.x) {
    //       this.player1_wins++
    //     } else {
    //       this.player2_wins++
    //     }
    //   } else if (this.tttList[1] === this.tttList[4] && this.tttList[4] === this.tttList[7] && this.tttList[1] !== null) {
    //     win_block.classList.add("open");
    //     if (!table.classList.contains("non-clickable-block")) {
    //       table.classList.add("non-clickable-block")
    //       btn.classList.remove("non-clickable-block")
    //     }
    //     this.winner = this.tttList[1] === this.x ? this.player1 : this.player2;
    //     if (this.tttList[1] === this.x) {
    //       this.player1_wins++
    //     } else {
    //       this.player2_wins++
    //     }
    //   } else if (this.tttList[2] === this.tttList[5] && this.tttList[5] === this.tttList[8] && this.tttList[2] !== null) {
    //     win_block.classList.add("open");
    //     if (!table.classList.contains("non-clickable-block")) {
    //       table.classList.add("non-clickable-block")
    //       btn.classList.remove("non-clickable-block")
    //     }
    //     this.winner = this.tttList[2] === this.x ? this.player1 : this.player2;
    //     if (this.tttList[2] === this.x) {
    //       this.player1_wins++
    //     } else {
    //       this.player2_wins++
    //     }
    //   } else if (this.tttList[2] === this.tttList[4] && this.tttList[4] === this.tttList[6] && this.tttList[2] !== null) {
    //     win_block.classList.add("open");
    //     if (!table.classList.contains("non-clickable-block")) {
    //       table.classList.add("non-clickable-block")
    //       btn.classList.remove("non-clickable-block")
    //     }
    //     this.winner = this.tttList[2] === this.x ? this.player1 : this.player2;
    //     if (this.tttList[2] === this.x) {
    //       this.player1_wins++
    //     } else {
    //       this.player2_wins++
    //     }
    //   } else if (this.tttList[3] === this.tttList[4] && this.tttList[4] === this.tttList[5] && this.tttList[3] !== null) {
    //     win_block.classList.add("open");
    //     if (!table.classList.contains("non-clickable-block")) {
    //       table.classList.add("non-clickable-block")
    //       btn.classList.remove("non-clickable-block")
    //     }
    //     this.winner = this.tttList[3] === this.x ? this.player1 : this.player2;
    //     if (this.tttList[3] === this.x) {
    //       this.player1_wins++
    //     } else {
    //       this.player2_wins++
    //     }
    //   } else if (this.tttList[6] === this.tttList[7] && this.tttList[7] === this.tttList[8] && this.tttList[6] !== null) {
    //     win_block.classList.add("open");
    //     if (!table.classList.contains("non-clickable-block")) {
    //       table.classList.add("non-clickable-block")
    //       btn.classList.remove("non-clickable-block")
    //     }
    //     this.winner = this.tttList[6] === this.x ? this.player1 : this.player2;
    //     if (this.tttList[6] === this.x) {
    //       this.player1_wins++
    //     } else {
    //       this.player2_wins++
    //     }
    //   } else if (this.tttList[2] === this.tttList[5] && this.tttList[5] === this.tttList[8] && this.tttList[2] !== null) {
    //     win_block.classList.add("open");
    //     if (!table.classList.contains("non-clickable-block")) {
    //       table.classList.add("non-clickable-block")
    //       btn.classList.remove("non-clickable-block")
    //     }
    //     this.winner = this.tttList[2] === this.x ? this.player1 : this.player2;
    //     if (this.tttList[2] === this.x) {
    //       this.player1_wins++
    //     } else {
    //       this.player2_wins++
    //     }
    //   } else if (!this.tttList.includes(null)) {
    //     text.innerText = 'Ничья!'
    //     win_block.classList.add("open");
    //     if (!table.classList.contains("non-clickable-block")) {
    //       table.classList.add("non-clickable-block")
    //       btn.classList.remove("non-clickable-block")
    //     }
    //   }
    // },
    fillList() {
      const win_block = document.querySelector(".win-block")
      const table = document.querySelector(".ttt__body-tbl")
      const btn = document.querySelector(".ttt-footer button")
      this.tttList.fill(null)

      if (win_block.classList.contains("open")) {
        win_block.classList.remove("open")
        if (table.classList.contains("non-clickable-block")) {
          table.classList.remove("non-clickable-block")
          btn.classList.remove("non-clickable-block")
        }
      }

      this.changePlayer('o')
      this.timePlayer1 = 30;
      this.timePlayer2 = 30;

      if (this.change) {
        const changePlayer1 = this.player1;
        const changePlayer2 = this.player2;
        const changeWin1 = this.player1_wins;
        const changeWin2 = this.player2_wins;
        this.change = false;
        this.player1 = changePlayer2;
        this.player2 = changePlayer1;
        this.player1_wins = changeWin2;
        this.player2_wins = changeWin1;
      }
      this.startTimer()
    },
    openName2() {
      const player1_section = document.querySelector(".player-1__container")
      const player2_section = document.querySelector(".player-2__container")
      if (player1_section.classList.contains("open")) {
        player1_section.classList.remove("open")
        player2_section.classList.add("open")
      }
    },
    openGame() {
      const player2_section = document.querySelector(".player-2__container")
      const players_section = document.querySelector(".input-name-container")
      const table = document.querySelector(".ttt__body-tbl")
      const btn = document.querySelector(".ttt-footer button")
      if (players_section.classList.contains("open") && player2_section.classList.contains("open")) {
        players_section.classList.remove("open")
        player2_section.classList.remove("open")
        table.classList.remove("non-clickable-block")
        btn.classList.remove("non-clickable-block")
        this.timePlayer1 = 30;
        this.timePlayer2 = 30;
        this.currentStep = 'x'
        this.startTimer()
      }
    },
    updatePlayerWins(winner) {
      this.currentStep = '';
      this.winner = winner
      if (winner === this.player2) {
        this.player2_wins++;
      } else if (winner === this.player1) {
        this.player1_wins++;
      } else {

      }
      this.stopTimer()
    },

    openStartOver(bool) {
      const btn = document.querySelector(".start__over")
      if (!btn.classList.contains("open")) {
        btn.classList.add("open")
      }
      this.change = !!bool;
    }
  },
  computed: {},
}

</script>

<template>
  <div class="container" v-cloak>
    <div class="ttt-column">
      <Header
          :player1="player1"
          :player2="player2"
          :player1_wins="player1_wins"
          :player2_wins="player2_wins"
          :timer-player1="timePlayer1"
          :timer-player2="timePlayer2"
      />
      <Game
          ref="game"
          :tttList="tttList"
          :current-step="currentStep"
          :x="x"
          :o="o"
          :is-hovered="isHovered"
          :select-cell="selectCell"
          :player1="player1"
          :player2="player2"
          @winner-updated="updatePlayerWins"
      />
      <!--      <div class="ttt__body">-->
      <!--        <table class="ttt__body-tbl non-clickable-block">-->
      <!--          <tr>-->
      <!--            <td class="tbl-1-1">-->
      <!--              <button-->
      <!--                  @mouseover="tttList[0] === null ? (changeFocus(0)) : null"-->
      <!--                  @mouseleave="resetFocus(0)"-->
      <!--                  @click="tttList[0] === null ? (selectCell(0)) : null">-->
      <!--                <img v-if="isHovered[0] && this.currentStep === 'x'" :src="this.x" alt="Крестик"/>-->
      <!--                <img v-else-if="isHovered[0] && currentStep === 'o'" :src="o" alt="Нолик"/>-->
      <!--                <img v-else :src="tttList[0]" alt=""/>-->
      <!--              </button>-->
      <!--            </td>-->
      <!--            <td class="tbl-1-2">-->
      <!--              <button-->
      <!--                  @mouseover="tttList[1] === null ? (changeFocus(1)) : null"-->
      <!--                  @mouseleave="resetFocus(1)"-->
      <!--                  @click="tttList[1] === null ? (selectCell(1)) : null">-->
      <!--                <img v-if="isHovered[1] && currentStep === 'x'" :src="x" alt="Крестик"/>-->
      <!--                <img v-else-if="isHovered[1] && currentStep === 'o'" :src="o" alt="Нолик"/>-->
      <!--                <img v-else :src="tttList[1]" alt=""/>-->
      <!--              </button>-->
      <!--            </td>-->
      <!--            <td class="tbl-1-3">-->
      <!--              <button-->
      <!--                  @mouseover="tttList[2] === null ? (changeFocus(2)) : null"-->
      <!--                  @mouseleave="resetFocus(2)"-->
      <!--                  @click="tttList[2] === null ? (selectCell(2)) : null">-->
      <!--                <img v-if="isHovered[2] && currentStep === 'x'" :src="x" alt="Крестик"/>-->
      <!--                <img v-else-if="isHovered[2] && currentStep === 'o'" :src="o" alt="Нолик"/>-->
      <!--                <img v-else :src="tttList[2]" alt=""/>-->
      <!--              </button>-->
      <!--            </td>-->
      <!--          </tr>-->
      <!--          <tr>-->
      <!--            <td class="tbl-2-1">-->
      <!--              <button-->
      <!--                  @mouseover="tttList[3] === null ? (changeFocus(3)) : null"-->
      <!--                  @mouseleave="resetFocus(3)"-->
      <!--                  @click="tttList[3] === null ? (selectCell(3)) : null">-->
      <!--                <img v-if="isHovered[3] && currentStep === 'x'" :src="x" alt="Крестик"/>-->
      <!--                <img v-else-if="isHovered[3] && currentStep === 'o'" :src="o" alt="Нолик"/>-->
      <!--                <img v-else :src="tttList[3]" alt=""/>-->
      <!--              </button>-->
      <!--            </td>-->
      <!--            <td class="tbl-2-2">-->
      <!--              <button-->
      <!--                  @mouseover="tttList[4] === null ? (changeFocus(4)) : null"-->
      <!--                  @mouseleave="resetFocus(4)"-->
      <!--                  @click="tttList[4] === null ? (selectCell(4)) : null">-->
      <!--                <img v-if="isHovered[4] && currentStep === 'x'" :src="x" alt="Крестик"/>-->
      <!--                <img v-else-if="isHovered[4] && currentStep === 'o'" :src="o" alt="Нолик"/>-->
      <!--                <img v-else :src="tttList[4]" alt=""/>-->
      <!--              </button>-->
      <!--            </td>-->
      <!--            <td class="tbl-2-3">-->
      <!--              <button-->
      <!--                  @mouseover="tttList[5] === null ? (changeFocus(5)) : null"-->
      <!--                  @mouseleave="resetFocus(5)"-->
      <!--                  @click="tttList[5] === null ? (selectCell(5)) : null">-->
      <!--                <img v-if="isHovered[5] && currentStep === 'x'" :src="x" alt="Крестик"/>-->
      <!--                <img v-else-if="isHovered[5] && currentStep === 'o'" :src="o" alt="Нолик"/>-->
      <!--                <img v-else :src="tttList[5]" alt=""/>-->
      <!--              </button>-->
      <!--            </td>-->
      <!--          </tr>-->
      <!--          <tr>-->
      <!--            <td class="tbl-3-1">-->
      <!--              <button-->
      <!--                  @mouseover="tttList[6] === null ? (changeFocus(6)) : null"-->
      <!--                  @mouseleave="resetFocus(6)"-->
      <!--                  @click="tttList[6] === null ? (selectCell(6)) : null">-->
      <!--                <img v-if="isHovered[6] && currentStep === 'x'" :src="x" alt="Крестик"/>-->
      <!--                <img v-else-if="isHovered[6] && currentStep === 'o'" :src="o" alt="Нолик"/>-->
      <!--                <img v-else :src="tttList[6]" alt=""/>-->
      <!--              </button>-->
      <!--            </td>-->
      <!--            <td class="tbl-3-2">-->
      <!--              <button-->
      <!--                  @mouseover="tttList[7] === null ? (changeFocus(7)) : null"-->
      <!--                  @mouseleave="resetFocus(7)"-->
      <!--                  @click="tttList[7] === null ? (selectCell(7)) : null">-->
      <!--                <img v-if="isHovered[7] && currentStep === 'x'" :src="x" alt="Крестик"/>-->
      <!--                <img v-else-if="isHovered[7] && currentStep === 'o'" :src="o" alt="Нолик"/>-->
      <!--                <img v-else :src="tttList[7]" alt=""/>-->
      <!--              </button>-->
      <!--            </td>-->
      <!--            <td class="tbl-3-3">-->
      <!--              <button-->
      <!--                  @mouseover="tttList[8] === null ? (changeFocus(8)) : null"-->
      <!--                  @mouseleave="resetFocus(8)"-->
      <!--                  @click="tttList[8] === null ? (selectCell(8)) : null">-->
      <!--                <img v-if="isHovered[8] && currentStep === 'x'" :src="x" alt="Крестик"/>-->
      <!--                <img v-else-if="isHovered[8] && currentStep === 'o'" :src="o" alt="Нолик"/>-->
      <!--                <img v-else :src="tttList[8]" alt=""/>-->
      <!--              </button>-->
      <!--            </td>-->
      <!--          </tr>-->
      <!--        </table>-->
      <!--      </div>-->
      <div class="win-block">
        <h2 v-if="this.winner.length > 0">Выиграл(а) <br/> {{ winner }}</h2>
        <h2 v-else>Ничья!</h2>
        <div class="imgs-container">
          <div class="medal-container">
            <img src="/cup.png" alt="Кубок"
                 class="medal-img">
          </div>
        </div>
        <div class="change">
          <span>Меняемся?</span>
          <div class="change-btns">
            <button @click="openStartOver(true)">Да</button>
            <button @click="openStartOver(false)">Нет</button>
          </div>
        </div>
        <button @click="fillList" class="start__over">Начать заново</button>
      </div>
      <div class="input-name-container open">
        <div class="player-1__container open">
          <h2 class="player-1__name">Игрок 1,<br/>представьтесь</h2>
          <input type="text" class="player-1__input" placeholder="Как вас зовут?" v-model="player1" minlength="1"
                 @keypress.enter="openName2">
          <button @click="openName2" class="player1__btn">Продолжить</button>
        </div>
        <div class="player-2__container">
          <h2 class="player-1__name">Игрок 2,<br/>представьтесь</h2>
          <input type="text" class="player-1__input" placeholder="Как вас зовут?" v-model="player2" minlength="1"
                 @keypress.enter="openGame">
          <button @click="openGame" class="player2__btn">Начать игру</button>
        </div>
      </div>
      <Footer :fill-list="fillList"/>
    </div>
  </div>
</template>

<style scoped>

</style>
