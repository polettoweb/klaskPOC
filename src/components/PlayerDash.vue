<template>
  <div class="dashboard__player">
    {{ name }}
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
  props: {
    name: String,
    id: Number
  }
};
</script>

<style lang="scss">
.dashboard {
  &__player {
    width: 200px;
    height: 40px;
  }
}
</style>