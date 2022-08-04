<template>
  <div class="table-grid">
    <div class="table-grid__item">
     <div @click="sortCompany" class="table-grid__item-company bold">Название</div>
     <div @click="sortName" class="table-grid__item-name bold">Фио директора</div>
     <div class="table-grid__item-phone bold">Телефон</div>
      <div class="table-grid__item-delete "></div>
    </div>
    <transition-group name="list">
      <t-item
          v-for="item in items"
          :key="item.id"
          :item="item"
          @delete-item="deleteItem"
      />
    </transition-group>
  </div>
</template>

<script>
import TItem from "@/components/tItem";
export default {
  name: "tTable",
  components: {TItem},
  props: {
    items: {
      type: Array,
      default: () => [],
    }
  },
  methods: {
    deleteItem(value) {
      this.$emit('delete-item', value)
    },
    sortCompany(){
      this.$emit('sort-name', 'company')
    },
    sortName(){
      this.$emit('sort-name', 'name')
    }
  }
}
</script>

<style lang="scss">
.bold {
  font-weight: 600;
}
  .table-grid {
    display: grid;
    grid-template-rows: auto;
    grid-template-columns: 1fr;
    width: 100%;
    border: 1px solid black;
    border-radius: 16px;
    margin-top: 30px;
    box-shadow: 5px 5px 20px rgba(187, 187, 187, 0.71);
    &__item {
      display: grid;
      grid-template-columns: 1fr 1fr 1fr 40px;
      grid-template-rows: 1fr;
      width: 100%;
      text-align: center;
      margin-top: -1px;
      &-name,&-company,&-phone,&-delete {
        border-right: 1px solid black;
        border-bottom: 1px solid black;
        padding: 15px 0px;
      }
      &-delete {
        border-right: none;
        cursor: pointer;
      }
    }
    &__item:last-child div{
        border-bottom: none;
    }

  }
.list-enter-active,
.list-leave-active {
  transition: all 1s ease;
}
.list-enter-from,
.list-leave-to,
.list-enter {
  opacity: 0;
  transform: translateY(30px);
}
.list-move {
  transition: transform 1s;
}
</style>