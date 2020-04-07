<template>
  <div>
    <div class="form__container">
      <div class="form__group field">
        <input
          type="input"
          class="form__field"
          placeholder="Add Player"
          name="addPlayer"
          autofocus
          v-model="playerName"
          @focus="showError = false"
        />
        <label for="addPlayer" :class="['form__label', { error: showError }]"
          >Add Player</label
        >
        <p v-show="showError" class="form__error">Please, fill the input</p>
      </div>
      <button
        type="button"
        aria-label="Add Player"
        :class="['form__submit', { green: added }]"
        @click="handlePlayerSubmit(id)"
      >
        ADD
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      added: false,
      showError: false,
      playerName: ""
    };
  },
  props: {
    id: Number
  },

  methods: {
    handlePlayerSubmit(id) {
      if (this.playerName == "") {
        this.showError = true;
      } else {
        this.added = true;
        let game = JSON.parse(localStorage.getItem("game") || "[]");
        game.push({ id: id, name: this.playerName });
        localStorage.setItem("game", JSON.stringify(game));
      }
    }
  }
};
</script>

<style lang="scss">
$max-width: 1080px;
$gray: #9b9b9b;

.form {
  &__container {
    width: 100%;
    max-width: $max-width;
    margin: 0 auto;
    height: 120px;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  &__group {
    position: relative;
    padding: 15px 0 0;
    margin-top: 10px;
    width: 70%;
  }

  &__field {
    font-family: inherit;
    width: 100%;
    border: 0;
    border-bottom: 2px solid $gray;
    outline: 0;
    font-size: 1.3rem;
    color: black;
    padding: 7px 0;
    background: transparent;
    transition: border-color 0.2s;

    &::placeholder {
      color: transparent;
    }
    &::-ms-input-placeholder {
      color: transparent;
    }

    &:placeholder-shown ~ .form__label {
      font-size: 1.3rem;
      cursor: text;
      top: 20px;
    }
  }

  &__field:focus {
    padding-bottom: 6px;
    font-weight: 700;
    border-width: 3px;
    border-color: $gray;
    border-image-slice: 1;

    ~ .form__label {
      position: absolute;
      top: 0;
      display: block;
      transition: 0.2s;
      font-size: 1rem;
      color: $gray;
      font-weight: 700;
    }
  }

  &__label {
    position: absolute;
    top: 0;
    display: block;
    transition: 0.2s;
    font-size: 1rem;
    color: $gray;

    &.error {
      color: red;
    }
  }

  &__error {
    color: red;
    text-align: left;
    position: absolute;
    bottom: -50px;
    left: 0;
  }

  &__submit {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-left: 10px;
    width: 62px;
    height: 62px;
    font-size: 20px;
    background-color: transparent;
    color: $gray;
    border-radius: 5px;
    border: 2px solid $gray;

    &.green {
      background-color: green;
      color: white;
    }
  }
}
</style>