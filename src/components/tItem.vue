<template>
  <div class="table-grid__item">
    <div class="table-grid__item-company">{{ item.company }}</div>
    <div class="table-grid__item-name">{{ item.name }}</div>
    <div class="table-grid__item-phone">{{ item.phone }}</div>
    <div @click="deleteItem" class="table-grid__item-delete">&#10060;</div>
  </div>
</template>

<script>
export default {
  name: "tItem",
  props: {
    item: {
      type: Object,
      default: () => {},
    },
  },
  methods: {
    deleteItem() {
      this.$emit("delete-item", this.item.id);
    },
  },
};
</script>

<style scoped></style>
