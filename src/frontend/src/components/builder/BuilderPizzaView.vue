<template>
  <div class="content__constructor">
    <div :class="`pizza pizza--foundation--${sizeClass}-${sauceClass}`">
      <div class="pizza__wrapper">
        <div
          v-for="ingredient in currentIngredients.filter(
            (item) => item.count > 0
          )"
          :key="ingredient.id"
          :class="`pizza__filling pizza__filling--${ingredientClass(
            ingredient.id
          )}`"
        ></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "BuilderPizzaView",
  props: {
    currentIngredients: {
      type: Array,
    },
    currentSauce: {
      type: Number,
      default: 1,
    },
    currentSize: {
      type: Number,
      default: 1,
    },
  },
  computed: {
    sizeClass: function () {
      switch (this.currentSize) {
        case 1:
          return "small";
        case 2:
          return "normal";
        case 3:
          return "big";
        default:
          return null;
      }
    },
    sauceClass: function () {
      switch (this.currentSauce) {
        case 1:
          return "tomato";
        case 2:
          return "creamy";
        default:
          return null;
      }
    },
  },
  methods: {
    ingredientClass(id) {
      switch (id) {
        case 1:
          return "mushrooms";
        case 2:
          return "cheddar";
        case 3:
          return "salami";
        case 4:
          return "ham";
        case 5:
          return "ananas";
        case 6:
          return "bacon";
        case 7:
          return "onion";
        case 8:
          return "chile";
        case 9:
          return "jalapeno";
        case 10:
          return "olives";
        case 11:
          return "tomatoes";
        case 12:
          return "salmon";
        case 13:
          return "mozzarella";
        case 14:
          return "parmezan";
        case 15:
          return "blue_cheese";
        default:
          return null;
      }
    },
  },
};
</script>

<style scoped></style>
