<template>
  <div>
    <header class="header">
      <div class="header__logo">
        <a href="#" class="logo">
          <img
            src="../assets/img/logo.svg"
            alt="V!U!E! Pizza logo"
            width="90"
            height="40"
          />
        </a>
      </div>
      <div class="header__cart">
        <a href="#">0 ₽</a>
      </div>
      <div class="header__user">
        <a href="#" class="header__login"><span>Войти</span></a>
      </div>
    </header>

    <main class="content">
      <form action="#" method="post">
        <div class="content__wrapper">
          <h1 class="title title--big">Конструктор пиццы</h1>

          <builder-dough-selector
            :dough="pizza.dough"
            :currentDough="currentPizza.dough"
            @setDough="currentPizza.dough = $event"
          />

          <div class="content__diameter">
            <div class="sheet">
              <h2 class="title title--small sheet__title">Выберите размер</h2>
              <radio-button
                :typeProp="'diameter'"
                :options="pizza.sizes"
                :current="currentPizza.size"
                @setCurrent="currentPizza.size = $event"
              />
            </div>
          </div>

          <div class="content__ingredients">
            <div class="sheet">
              <h2 class="title title--small sheet__title">
                Выберите ингредиенты
              </h2>

              <div class="sheet__content ingredients">
                <radio-button
                  title="Основной соус:"
                  :typeProp="'sauce'"
                  :options="pizza.sauces"
                  :current="currentPizza.sauce"
                  @setCurrent="currentPizza.sauce = $event"
                />

                <div class="ingredients__filling">
                  <p>Начинка:</p>

                  <ul class="ingredients__list">
                    <li
                      class="ingredients__item"
                      v-for="(ingredient, index) in pizza.ingredients"
                      :key="ingredient.id"
                    >
                      <selector-item :item="ingredient" />
                      <item-counter
                        :current="currentPizza.ingredients[index].count"
                      />
                    </li>
                  </ul>
                </div>
              </div>
            </div>
          </div>

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

            <div class="content__constructor">
              <div
                :class="`pizza pizza--foundation--${sizeClass(
                  currentPizza.size
                )}-${sauceClass(currentPizza.sauce)}`"
              >
                <div class="pizza__wrapper">
                  <div
                    v-for="ingredient in currentPizza.ingredients.filter(
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

            <div class="content__result">
              <p>Итого: {{ price }} ₽</p>
              <button type="button" class="button" :disabled="price === 0">
                Готовьте!
              </button>
            </div>
          </div>
        </div>
      </form>
    </main>
  </div>
</template>

<script>
import pizzaJson from "../static/pizza.json";

import ItemCounter from "../common/components/ItemCounter";
import SelectorItem from "../common/components/SelectorItem";
import RadioButton from "../common/components/RadioButton";
import BuilderDoughSelector from "../components/builder/BuilderDoughSelector";

export default {
  components: { BuilderDoughSelector, SelectorItem, RadioButton, ItemCounter },
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
  computed: {
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

<style></style>
