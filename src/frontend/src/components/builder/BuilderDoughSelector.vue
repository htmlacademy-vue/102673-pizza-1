<template>
  <div class="content__dough">
    <div class="sheet">
      <h2 class="title title--small sheet__title">Выберите тесто</h2>
      <radio-button
        :options="dough"
        :typeProp="'dough'"
        :current="currentDough"
        @setCurrent="setDough($event)"
      />
    </div>
  </div>
</template>

<script>
import RadioButton from "../../common/components/RadioButton";

export default {
  name: "BuilderDoughSelector",
  components: { RadioButton },
  props: {
    dough: {
      type: Array,
      required: true,
    },
    currentDough: {
      type: Number,
      default: 1,
      required: true,
    },
  },
  methods: {
    setDough(dough) {
      this.$emit("setDough", dough);
    },
  },
};
</script>

<style scoped></style>
