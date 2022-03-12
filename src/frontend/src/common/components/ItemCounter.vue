<template>
  <div class="counter counter--orange ingredients__counter">
    <button
      type="button"
      class="counter__button counter__button--minus"
      :disabled="isDisabled"
      @click="reduceCount"
    >
      <span class="visually-hidden">Меньше</span>
    </button>
    <input type="text" name="counter" class="counter__input" :value="current" />
    <button
      type="button"
      class="counter__button counter__button--plus"
      @click="increaseCount"
    >
      <span class="visually-hidden">Больше</span>
    </button>
  </div>
</template>

<script>
export default {
  name: "ItemCounter",
  props: {
    current: {
      type: Number,
      default: 0,
      required: true,
    },
  },
  methods: {
    increaseCount() {
      this.current++;
    },
    reduceCount() {
      this.current--;
    },
  },
  computed: {
    isDisabled: function () {
      return this.current === 0;
    },
  },
};
</script>

<style scoped></style>
