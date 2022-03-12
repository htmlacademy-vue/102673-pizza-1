<template>
  <div class="content__result">
    <p>Итого: {{ price }} ₽</p>
    <button type="button" class="button" :disabled="isDisabled">
      Готовьте!
    </button>
  </div>
</template>

<script>
import pizzaJson from "../../static/pizza.json";

export default {
  name: "BuilderPriceCounter",
  data() {
    return {
      pizza: pizzaJson,
    };
  },
  props: {
    currentPizza: {
      type: Object,
    },
  },
  computed: {
    isDisabled: function () {
      return this.price === 0;
    },
    price: function () {
      let priceDough,
        priceSauce,
        multiplierSize,
        priceIngredient = 0;

      priceDough = this.pizza.dough.filter(
        (item) => item.id === this.currentPizza.dough
      )[0].price;

      priceSauce = this.pizza.sauces.filter(
        (item) => item.id === this.currentPizza.sauce
      )[0].price;

      multiplierSize = this.pizza.sizes.filter(
        (item) => item.id === this.currentPizza.size
      )[0].multiplier;

      for (let ingredient of this.pizza.ingredients) {
        let countIngredient = this.currentPizza.ingredients.filter(
          (item) => item.id === ingredient.id
        )[0].count;

        if (countIngredient > 0) {
          priceIngredient += countIngredient * ingredient.price;
        }
      }
      return multiplierSize * (priceDough + priceSauce + priceIngredient);
    },
  },
};
</script>

<style scoped></style>
