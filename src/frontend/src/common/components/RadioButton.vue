<template>
  <div :class="this.classContainer()">
    <p v-if="title">{{ title }}</p>
    <label
      v-for="option in options"
      :key="option.id"
      :class="className(option.id)"
    >
      <input
        type="radio"
        class="visually-hidden"
        :name="typeProp"
        :value="option.id"
        @change="$emit('setCurrent', +$event.target.value)"
        v-model="current"
      />
      <template v-if="option.description">
        <b>{{ option.name }}</b>
        <span>{{ option.description }}</span>
      </template>
      <span v-else>{{ option.name }}</span>
    </label>
  </div>
</template>

<script>
export default {
  name: "RadioButton",
  props: {
    options: {
      type: Array,
      required: true,
    },
    typeProp: {
      type: String,
      required: true,
    },
    current: {
      type: Number,
    },
    title: {
      type: String,
    },
  },
  methods: {
    doughClass(id) {
      switch (id) {
        case 1:
          return "light";
        case 2:
          return "large";
        default:
          return null;
      }
    },
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
    className(id) {
      switch (this.typeProp) {
        case "dough":
          return `${this.typeProp}__input ${
            this.typeProp
          }__input--${this.doughClass(id)}`;
        case "diameter":
          return `${this.typeProp}__input ${
            this.typeProp
          }__input--${this.sizeClass(id)}`;
        case "sauce":
          return "radio ingredients__input";
        default:
          return null;
      }
    },
    classContainer() {
      switch (this.typeProp) {
        case "dough":
        case "diameter":
          return `sheet__content ${this.typeProp}`;
        case "sauce":
          return `ingredients__${this.typeProp}`;
        default:
          return null;
      }
    },
  },
};
</script>
