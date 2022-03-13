<template>
  <div class="content__ingredients">
    <div class="sheet">
      <h2 class="title title--small sheet__title">Выберите ингредиенты</h2>

      <div class="sheet__content ingredients">
        <radio-button
          title="Основной соус:"
          :typeProp="'sauce'"
          :options="sauces"
          :current="currentSauce"
          @setCurrent="setSauce($event)"
        />

        <div class="ingredients__filling">
          <p>Начинка:</p>

          <ul class="ingredients__list">
            <li
              class="ingredients__item"
              v-for="(ingredient, index) in ingredients"
              :key="ingredient.id"
            >
              <selector-item :item="ingredient" />
              <item-counter
                :count="currentIngredients[index].count"
                @setCount="setIngredient($event, index)"
              />
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import RadioButton from "../../common/components/RadioButton";
import SelectorItem from "../../common/components/SelectorItem";
import ItemCounter from "../../common/components/ItemCounter";

export default {
  name: "BuilderIngredientsSelector",
  components: { RadioButton, SelectorItem, ItemCounter },
  props: {
    sauces: {
      type: Array,
      required: true,
    },
    currentSauce: {
      type: Number,
      required: true,
      default: 1,
    },
    ingredients: {
      type: Array,
      required: true,
    },
    currentIngredients: {
      type: Array,
    },
  },
  methods: {
    setSauce(sauce) {
      this.$emit("setSauce", sauce);
    },
    setIngredient(count, index) {
      this.$emit("setIngredient", { count: count, index: index });
    },
  },
};
</script>

<style scoped></style>
