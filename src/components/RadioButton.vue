<template>
  <div class="radio">
    <div v-for="(item, index) in data" :key="index" class="radio-button">
      <label>
        <input type="radio" :value="item.id" v-model="innerValue" />
        {{ item.label }}
      </label>
    </div>
  </div>
</template>

<script>
export default {
  name: "RadioButton",
  props: {
    value: Number,
    id: Number,
    data: Array,
  },
  computed: {
    innerValue: {
      get() {
        return this.value;
      },
      set(value) {
        this.$emit("change-value", this.id, Number(value));
      },
    },
  },
};
</script>

<style lang="scss" scoped>
.radio {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  &-button {
    margin-right: 8px;
  }
}
</style>