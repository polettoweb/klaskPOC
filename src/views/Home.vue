<template>
  <div class="home">
    <img alt="Klask logo" src="../assets/klask.png" />
    <div class="dashboard"></div>
    <div v-if="players.length" class="dashboard__grid">
      <PlayerDash
        v-for="player in players"
        :key="player.id"
        :name="player.name"
        :id="player.id"
      />
    </div>
    <div v-else>
      <p>Please create a new match</p>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import PlayerDash from "@/components/PlayerDash";
export default {
  name: "Dashboard",
  components: {
    // HelloWorld
    PlayerDash
  },
  data() {
    return {
      players: localStorage.getItem("game")
        ? JSON.parse(localStorage.getItem("game"))
        : []
    };
  },
  computed: {
    numberOfSections() {
      return this.players.length / 2;
    }
  },
  mounted() {
    if (localStorage.getItem("game")) {
      if (this.players.length > 1) {
        console.log(this.numberOfSections);
      }
    }
  }
};
</script>
<style lang="scss">
.dashboard {
  &__grid {
    display: grid;
  }
}
</style>
