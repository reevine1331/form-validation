<template>
  <select v-model="innerValue">
    <option v-for="(item, index) in data" :key="index" :value="item.id">
      {{ item.label }}
    </option>
  </select>
</template>

<script>
export default {
  name: "SelectBox",
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
select {
  border: none;
  border-bottom: 1px solid gray;
  outline: none;
  height: 24px;
  font-size: 16px;
}
</style>