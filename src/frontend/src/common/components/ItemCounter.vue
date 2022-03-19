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
    <input
      type="text"
      name="counter"
      class="counter__input"
      :value="countData"
      @input="countData = $event.target.value"
    />
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
  data() {
    return {
      countData: this.count,
    };
  },
  props: {
    count: {
      type: Number,
      default: 0,
      required: true,
    },
  },
  methods: {
    increaseCount() {
      this.countData++;
      this.$emit("setCount", this.countData);
    },
    reduceCount() {
      this.countData--;
      this.$emit("setCount", this.countData);
    },
  },
  computed: {
    isDisabled: function () {
      return this.countData === 0;
    },
  },
};
</script>

<style scoped></style>
