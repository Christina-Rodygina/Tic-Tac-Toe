<script>
  export default {
    props: {
      fillList: Function
    }
  }
</script>

<template>
  <footer class="ttt-footer">
    <button class="non-clickable-block" @click="fillList">Прервать игру</button>
  </footer>
</template>

<style scoped>

</style>