<script>
  export default {
    props: {
      tttList: Array,
      currentStep: String,
      x: String,
      o: String,
      isHovered: Array,
      selectCell: Function,
      player1: String,
      player2: String,
    },
    methods: {
      changeFocus(index) {
        if (!this.tttList[index]) {
          this.isHovered[index] = true;
        }
      },
      resetFocus(index) {
        this.isHovered[index] = false;
      },
      checkingWin() {
        const win_block = document.querySelector(".win-block")
        const table = document.querySelector(".ttt__body-tbl")
        const btn = document.querySelector(".ttt-footer button")
        if (this.tttList[0] === this.tttList[1] && this.tttList[1] === this.tttList[2] && this.tttList[0] !== null) {
          win_block.classList.add("open");
          if (!table.classList.contains("non-clickable-block")) {
            table.classList.add("non-clickable-block")
            btn.classList.remove("non-clickable-block")
          }
          const winner = this.tttList[0] === this.x ? this.player1 : this.player2;
          this.$emit('winner-updated', winner);
        } else if (this.tttList[0] === this.tttList[4] && this.tttList[4] === this.tttList[8] && this.tttList[0] !== null) {
          win_block.classList.add("open");
          if (!table.classList.contains("non-clickable-block")) {
            table.classList.add("non-clickable-block")
          }
          const winner = this.tttList[0] === this.x ? this.player1 : this.player2;
          this.$emit('winner-updated', winner);
        } else if (this.tttList[0] === this.tttList[3] && this.tttList[3] === this.tttList[6] && this.tttList[0] !== null) {
          win_block.classList.add("open");
          if (!table.classList.contains("non-clickable-block")) {
            table.classList.add("non-clickable-block")
            btn.classList.remove("non-clickable-block")
          }
          const winner = this.tttList[0] === this.x ? this.player1 : this.player2;
          this.$emit('winner-updated', winner);
        } else if (this.tttList[1] === this.tttList[4] && this.tttList[4] === this.tttList[7] && this.tttList[1] !== null) {
          win_block.classList.add("open");
          if (!table.classList.contains("non-clickable-block")) {
            table.classList.add("non-clickable-block")
            btn.classList.remove("non-clickable-block")
          }
          const winner = this.tttList[1] === this.x ? this.player1 : this.player2;
          this.$emit('winner-updated', winner);
        } else if (this.tttList[2] === this.tttList[5] && this.tttList[5] === this.tttList[8] && this.tttList[2] !== null) {
          win_block.classList.add("open");
          if (!table.classList.contains("non-clickable-block")) {
            table.classList.add("non-clickable-block")
            btn.classList.remove("non-clickable-block")
          }
          const winner = this.tttList[2] === this.x ? this.player1 : this.player2;
          this.$emit('winner-updated', winner);
        } else if (this.tttList[2] === this.tttList[4] && this.tttList[4] === this.tttList[6] && this.tttList[2] !== null) {
          win_block.classList.add("open");
          if (!table.classList.contains("non-clickable-block")) {
            table.classList.add("non-clickable-block")
            btn.classList.remove("non-clickable-block")
          }
          const winner = this.tttList[2] === this.x ? this.player1 : this.player2;
          this.$emit('winner-updated', winner);
        } else if (this.tttList[3] === this.tttList[4] && this.tttList[4] === this.tttList[5] && this.tttList[3] !== null) {
          win_block.classList.add("open");
          if (!table.classList.contains("non-clickable-block")) {
            table.classList.add("non-clickable-block")
            btn.classList.remove("non-clickable-block")
          }
          const winner = this.tttList[3] === this.x ? this.player1 : this.player2;
          this.$emit('winner-updated', winner);
        } else if (this.tttList[6] === this.tttList[7] && this.tttList[7] === this.tttList[8] && this.tttList[6] !== null) {
          win_block.classList.add("open");
          if (!table.classList.contains("non-clickable-block")) {
            table.classList.add("non-clickable-block")
            btn.classList.remove("non-clickable-block")
          }
          const winner = this.tttList[6] === this.x ? this.player1 : this.player2;
          this.$emit('winner-updated', winner);
        } else if (this.tttList[2] === this.tttList[5] && this.tttList[5] === this.tttList[8] && this.tttList[2] !== null) {
          win_block.classList.add("open");
          if (!table.classList.contains("non-clickable-block")) {
            table.classList.add("non-clickable-block")
            btn.classList.remove("non-clickable-block")
          }
          const winner = this.tttList[2] === this.x ? this.player1 : this.player2;
          this.$emit('winner-updated', winner);
        } else if (!this.tttList.includes(null)) {
          // text.innerText = 'Ничья!'
          win_block.classList.add("open");
          if (!table.classList.contains("non-clickable-block")) {
            table.classList.add("non-clickable-block")
            btn.classList.remove("non-clickable-block")
          }
          const winner = '';
          this.$emit('winner-updated', winner);
        }
      }
    }
  }
</script>

<template>
  <div class="ttt__body">
    <table class="ttt__body-tbl non-clickable-block">
      <tr>
        <td class="tbl-1-1">
          <button
              @mouseover="tttList[0] === null ? (changeFocus(0)) : null"
              @mouseleave="resetFocus(0)"
              @click="tttList[0] === null ? (selectCell(0)) : null">
            <img v-if="isHovered[0] && currentStep === 'x'" :src="x" alt="Крестик"/>
            <img v-else-if="isHovered[0] && currentStep === 'o'" :src="o" alt="Нолик"/>
            <img v-else :src="tttList[0]" alt=""/>
          </button>
        </td>
        <td class="tbl-1-2">
          <button
              @mouseover="tttList[1] === null ? (changeFocus(1)) : null"
              @mouseleave="resetFocus(1)"
              @click="tttList[1] === null ? (selectCell(1)) : null">
            <img v-if="isHovered[1] && currentStep === 'x'" :src="x" alt="Крестик"/>
            <img v-else-if="isHovered[1] && currentStep === 'o'" :src="o" alt="Нолик"/>
            <img v-else :src="tttList[1]" alt=""/>
          </button>
        </td>
        <td class="tbl-1-3">
          <button
              @mouseover="tttList[2] === null ? (changeFocus(2)) : null"
              @mouseleave="resetFocus(2)"
              @click="tttList[2] === null ? (selectCell(2)) : null">
            <img v-if="isHovered[2] && currentStep === 'x'" :src="x" alt="Крестик"/>
            <img v-else-if="isHovered[2] && currentStep === 'o'" :src="o" alt="Нолик"/>
            <img v-else :src="tttList[2]" alt=""/>
          </button>
        </td>
      </tr>
      <tr>
        <td class="tbl-2-1">
          <button
              @mouseover="tttList[3] === null ? (changeFocus(3)) : null"
              @mouseleave="resetFocus(3)"
              @click="tttList[3] === null ? (selectCell(3)) : null">
            <img v-if="isHovered[3] && currentStep === 'x'" :src="x" alt="Крестик"/>
            <img v-else-if="isHovered[3] && currentStep === 'o'" :src="o" alt="Нолик"/>
            <img v-else :src="tttList[3]" alt=""/>
          </button>
        </td>
        <td class="tbl-2-2">
          <button
              @mouseover="tttList[4] === null ? (changeFocus(4)) : null"
              @mouseleave="resetFocus(4)"
              @click="tttList[4] === null ? (selectCell(4)) : null">
            <img v-if="isHovered[4] && currentStep === 'x'" :src="x" alt="Крестик"/>
            <img v-else-if="isHovered[4] && currentStep === 'o'" :src="o" alt="Нолик"/>
            <img v-else :src="tttList[4]" alt=""/>
          </button>
        </td>
        <td class="tbl-2-3">
          <button
              @mouseover="tttList[5] === null ? (changeFocus(5)) : null"
              @mouseleave="resetFocus(5)"
              @click="tttList[5] === null ? (selectCell(5)) : null">
            <img v-if="isHovered[5] && currentStep === 'x'" :src="x" alt="Крестик"/>
            <img v-else-if="isHovered[5] && currentStep === 'o'" :src="o" alt="Нолик"/>
            <img v-else :src="tttList[5]" alt=""/>
          </button>
        </td>
      </tr>
      <tr>
        <td class="tbl-3-1">
          <button
              @mouseover="tttList[6] === null ? (changeFocus(6)) : null"
              @mouseleave="resetFocus(6)"
              @click="tttList[6] === null ? (selectCell(6)) : null">
            <img v-if="isHovered[6] && currentStep === 'x'" :src="x" alt="Крестик"/>
            <img v-else-if="isHovered[6] && currentStep === 'o'" :src="o" alt="Нолик"/>
            <img v-else :src="tttList[6]" alt=""/>
          </button>
        </td>
        <td class="tbl-3-2">
          <button
              @mouseover="tttList[7] === null ? (changeFocus(7)) : null"
              @mouseleave="resetFocus(7)"
              @click="tttList[7] === null ? (selectCell(7)) : null">
            <img v-if="isHovered[7] && currentStep === 'x'" :src="x" alt="Крестик"/>
            <img v-else-if="isHovered[7] && currentStep === 'o'" :src="o" alt="Нолик"/>
            <img v-else :src="tttList[7]" alt=""/>
          </button>
        </td>
        <td class="tbl-3-3">
          <button
              @mouseover="tttList[8] === null ? (changeFocus(8)) : null"
              @mouseleave="resetFocus(8)"
              @click="tttList[8] === null ? (selectCell(8)) : null">
            <img v-if="isHovered[8] && currentStep === 'x'" :src="x" alt="Крестик"/>
            <img v-else-if="isHovered[8] && currentStep === 'o'" :src="o" alt="Нолик"/>
            <img v-else :src="tttList[8]" alt=""/>
          </button>
        </td>
      </tr>
    </table>
  </div>
</template>

<style scoped>

</style>