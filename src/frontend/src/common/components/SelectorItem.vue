<template>
  <span :class="`filling filling--${ingredientClass(item.id)}`">{{
    item.name
  }}</span>
</template>

<script>
export default {
  name: "SelectorItem",
  props: {
    item: {
      type: Object,
      required: true,
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
          return "parmesan";
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
