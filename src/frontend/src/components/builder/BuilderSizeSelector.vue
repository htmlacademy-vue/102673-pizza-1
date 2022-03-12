<template>
  <div class="content__diameter">
    <div class="sheet">
      <h2 class="title title--small sheet__title">Выберите размер</h2>
      <radio-button
        :typeProp="'diameter'"
        :options="sizes"
        :current="currentSize"
        @setCurrent="setSize($event)"
      />
    </div>
  </div>
</template>

<script>
import RadioButton from "../../common/components/RadioButton";

export default {
  name: "BuilderSizeSelector",
  components: { RadioButton },
  props: {
    sizes: {
      type: Array,
      required: true,
    },
    currentSize: {
      type: Number,
      required: true,
      default: 3,
    },
  },
  methods: {
    setSize(size) {
      this.$emit("setSize", size);
    },
  },
};
</script>

<style scoped></style>
