<template>
  <div>
    <app-layout />

    <main class="content">
      <form action="#" method="post">
        <div class="content__wrapper">
          <h1 class="title title--big">Конструктор пиццы</h1>

          <builder-dough-selector
            :dough="pizza.dough"
            :currentDough="currentPizza.dough"
            @setDough="currentPizza.dough = $event"
          />

          <builder-size-selector
            :sizes="pizza.sizes"
            :currentSize="currentPizza.size"
            @setSize="currentPizza.size = $event"
          />

          <builder-ingredients-selector
            :sauces="pizza.sauces"
            :currentSauce="currentPizza.sauce"
            :ingredients="pizza.ingredients"
            :currentIngredients="currentPizza.ingredients"
            @setSauce="currentPizza.sauce = $event"
            @setIngredient="
              currentPizza.ingredients[$event.index].count = $event.count
            "
          />

          <div class="content__pizza">
            <label class="input">
              <span class="visually-hidden">Название пиццы</span>
              <input
                type="text"
                name="pizza_name"
                placeholder="Введите название пиццы"
                v-model="currentPizza.name"
              />
            </label>

            <div @dragover.prevent @dragenter.prevent @drop="onDrop($event)">
              <builder-pizza-view
                :currentSize="currentPizza.size"
                :currentSauce="currentPizza.sauce"
                :currentIngredients="currentPizza.ingredients"
              />
            </div>

            <builder-price-counter :currentPizza="currentPizza" />
          </div>
        </div>
      </form>
    </main>
  </div>
</template>

<script>
import pizzaJson from "../static/pizza.json";

import AppLayout from "../layouts/AppLayout";
import BuilderDoughSelector from "../components/builder/BuilderDoughSelector";
import BuilderSizeSelector from "../components/builder/BuilderSizeSelector";
import BuilderIngredientsSelector from "../components/builder/BuilderIngredientsSelector";
import BuilderPriceCounter from "../components/builder/BuilderPriceCounter";
import BuilderPizzaView from "../components/builder/BuilderPizzaView";

export default {
  components: {
    AppLayout,
    BuilderPizzaView,
    BuilderPriceCounter,
    BuilderIngredientsSelector,
    BuilderDoughSelector,
    BuilderSizeSelector,
  },
  data() {
    return {
      pizza: pizzaJson,
      currentPizza: {
        name: "Лучшая пицца",
        dough: 1,
        ingredients: [
          { id: 1, count: 0 },
          { id: 2, count: 2 },
          { id: 3, count: 0 },
          { id: 4, count: 0 },
          { id: 5, count: 1 },
          { id: 6, count: 3 },
          { id: 7, count: 0 },
          { id: 8, count: 0 },
          { id: 9, count: 0 },
          { id: 10, count: 0 },
          { id: 11, count: 0 },
          { id: 12, count: 0 },
          { id: 13, count: 0 },
          { id: 14, count: 0 },
          { id: 15, count: 0 },
        ],
        size: 3,
        sauce: 1,
      },
    };
  },
  methods: {
    sizeClass(id) {
      switch (id) {
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
    sauceClass(id) {
      switch (id) {
        case 1:
          return "tomato";
        case 2:
          return "creamy";
        default:
          return null;
      }
    },
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
    setIngredients(e) {
      this.currentPizza.ingredients[e.id].count = e.count;
    },
    onDrop(e) {
      if (!e) {
        return;
      }
      const ingredientId = parseInt(e.dataTransfer.getData("itemId"));
      this.currentPizza.ingredients.map((x) => {
        if (x.id === ingredientId) {
          x.count++;
        }
        return x;
      });
    },
  },
};
</script>
