<template>
  <div class="create">
    <h1>Create your tournament by adding as many players as you need</h1>
    <p>How many players do you want to add?</p>
    <select name="numberOfPlayers" @change="handleNumberOfPlayers">
      <option :value="0">0</option>
      <option :value="4">4</option>
      <option :value="8">8</option>
      <option :value="16">16</option>
    </select>
    <div v-if="showPlayerFields">
      <Player
        v-for="(player, index) in numberOfPlayers"
        :key="player"
        :id="index"
      />
      <button class="create__button" @click="handleCreateGame">
        Create Game
      </button>
    </div>
  </div>
</template>
<script>
import Player from "../components/Player";
export default {
  components: {
    Player
  },
  data() {
    return {
      showPlayerFields: false,
      numberOfPlayers: 0
    };
  },
  methods: {
    handleNumberOfPlayers(event) {
      this.numberOfPlayers = Number(event.target.value);
      if (this.numberOfPlayers > 0) {
        this.showPlayerFields = true;
        console.log(event.target.value);
        localStorage.clear();
        localStorage.setItem("game", []);
      }
    },
    handleCreateGame() {
      this.$router.push("/");
    }
  }
};
</script>
<style lang="scss">
.create {
  width: 80%;
  max-width: 800px;
  margin: 0 auto;

  &__button {
    display: block;
    width: 200px;
    height: 50px;
    margin: 20px auto;
  }
}
</style>
