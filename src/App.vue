<template>
  <div id="app">
    <div class="container">
      <div class="table-edit">
        <t-input v-model="name" :placeholder="'Найти по ФИО'"/>
        <t-button @click.native="openModal" :inner-text="'Добавить'"/>
      </div>
      <div class="table">
        <t-table
            @sort-name="sortName"
            @sort-company="sortName"
            @delete-item="deleteItem"
            :items="searchName"
        />
      </div>
      <div class="table-pagination">
        <div class="table-pagination__row">
          <div  :class="{'disabled':page < 2}" @click="page = page - 1" class="table-pagination__row-item button">&#10148;</div>
          <div class="table-pagination__row-item">Страница: {{page}}</div>
          <div :class="{'disabled': showNextButton}" @click="page = page + 1" class="table-pagination__row-item button">&#10148;</div>
        </div>
      </div>
    </div>
    <transition name="fade">
      <t-modal
          @close-modal="closeModal"
          v-if="showModal"
          @new-item="insertItem"
      />
    </transition>

  </div>
</template>

<script>

import TInput from "@/components/UI/tInput";
import TButton from "@/components/UI/tButton";
import TTable from "@/components/tTable";
import TModal from "@/components/tModal";
export default {
  name: "App",
  components: {
    TModal,
    TTable,
    TButton,
    TInput
  },
  data() {
    return {
      items: [
        {
          id: 1,
          name: 'Иванов М.А.',
          company: 'ООО Ростелеком1',
          phone: '+7 (999) 999-99-99'
        },
        {
          id: 2,
          name: 'Сидоров М.А.2',
          company: 'ВВВ Ростелеком2',
          phone: '+7 (999) 999-99-99'
        },
        {
          id: 3,
          name: 'Ахматов М.А.3',
          company: 'ААА Ростелеком3',
          phone: '+7 (999) 999-99-99'
        },
        {
          id: 7,
          name: 'Ахматов М.А.3',
          company: 'ААА Ростелеком3',
          phone: '+7 (999) 999-99-99'
        },
        {
          id: 4,
          name: 'Ахматов М.А.3',
          company: 'ААА Ростелеком3',
          phone: '+7 (999) 999-99-99'
        },
        {
          id: 5,
          name: 'Ахматов М.А.3',
          company: 'ААА Ростелеком3',
          phone: '+7 (999) 999-99-99'
        },
        {
          id: 6,
          name: 'Ахматов М.А.3',
          company: 'ААА Ростелеком3',
          phone: '+7 (999) 999-99-99'
        },
      ],
      showModal: false,
      page: 1,
      total: 0,
      name:'',
      newArr:[],
      hasNextPage: true,
    }
  },
  methods: {
    openModal() {
      this.showModal = true
    },
    closeModal(value) {
      this.showModal = value
    },
    insertItem(item) {
      this.items.push(item)
      localStorage.setItem('item', JSON.stringify(this.items))
      this.showModal = false
    },
    deleteItem(id) {
      this.items = this.items.filter((e) => e.id !== id)
      if(this.items.length === 6){
        this.page = 1
      }
      localStorage.setItem('item', JSON.stringify(this.items))
    },
    sortName(value) {
      if(value === 'name'){
        this.items.sort(function (a, b) {
          return a.name.localeCompare(b.name)
        })
      } else {
        this.items.sort(function (a, b) {
          return a.company.localeCompare(b.company)
        })
      }

    }
  },
  computed: {
    searchName() {
      const start = (this.page - 1) * 6
      const end = this.page * 6
      const filteredItems = this.items.filter(item => item.name.toLowerCase().includes(this.name.toLowerCase()))
      return filteredItems.slice(start,end)
    },
    showNextButton(){
      const end = this.page * 6
      if(this.items.length > end) {
        return false
      }
      return true
    }
  },
  mounted() {
    const itemsData = localStorage.getItem('item')
    if (itemsData) {
      this.items = JSON.parse(itemsData)
    }
  }
}
</script>

<style lang="scss">
@import '@/assets/style/nullstyle.scss';
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.container {
  max-width: 1200px;
  padding: 0px 16px;
  margin: 0 auto;
}
.table-edit {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  & label {
    margin-bottom: 0px;
  }
}
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active до версии 2.1.8 */ {
  opacity: 0;
}
.table-pagination {
  display: flex;
  flex-direction: row;
  justify-content: flex-end;
  width: 100%;
  margin-top: 30px;
  &__row {
    display: flex;
    flex-direction: row;
    align-items: center;
    max-width: 300px;
    width: 100%;
    &-item {
      width: 100%;
      transition: all 0.4s ease;
    }
    &-item:first-child, &-item:last-child {
      cursor: pointer;
      padding: 10px 0px;
      border-radius: 5px;

    }
    &-item:first-child {
      transform: rotate(180deg);
    }
  }
}
.disabled {
  pointer-events: none;
  cursor: none;
}
</style>
