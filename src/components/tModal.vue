<template>
  <div class="modal">
    <div class="modal-container">
      <div class="input-group">
        <t-input
            :type="'text'"
            v-model="$v.newItem.company.$model"
            :placeholder="'Название'"
            :className="{'error': ($v.newItem.company.$dirty && !$v.newItem.company.required)}"
        />
        <t-input
            :type="'text'"
            :placeholder="'Фио директора'"
            v-model="$v.newItem.name.$model"
            :className="{'error': ($v.newItem.name.$dirty && $v.newItem.name.$invalid)}"
        />
        <t-input
            :type="'phone'"
            v-model="$v.newItem.phone.$model"
            :placeholder="'Номер телефона'"
            :className="{'error': ($v.newItem.phone.$dirty && $v.newItem.phone.$invalid)}"
            :class="'input'"
        />
      </div>
      <div class="modal-buttons">
        <t-button @click.native="closeModal" :class-name="{'red': true}" :inner-text="'Отменить'"/>
        <t-button
            @click.native="setNewItem"
            :inner-text="'Добавить'"
            :className="{'disabled': $v.$invalid}"
        />
      </div>
    </div>
  </div>
</template>

<script>
import TButton from "@/components/UI/tButton";
import TInput from "@/components/UI/tInput";
import { validationMixin } from 'vuelidate';
import { required,minLength} from 'vuelidate/lib/validators';

export default {
  name: "tModal",
  mixins: [validationMixin],
  components: {TInput, TButton},
  data() {
    return {
      newItem: {
        name:'',
        company:'',
        phone:'',
      },
      error: true,
    }
  },
  validations: {
    newItem: {
      name: { required },
      company: { required },
      phone: { required,minLength: minLength(12) },
    },
  },
  methods: {
    closeModal() {
      this.$emit('close-modal', false)
    },
    setNewItem(){
      this.newItem.name
      this.newItem.company
      this.newItem.phone
      this.newItem.id = Date.now()
      this.$emit('new-item', this.newItem)
      this.newItem = {}
    },
  },
}
</script>

<style scoped lang="scss">
.modal {
  position: fixed;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  z-index: 2;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0,0,0,0.5);
  &-container {
    position: relative;
    max-width: 500px;
    width: 100%;
    background: white;
    border-radius: 16px;
    padding: 20px;
  }
  &-buttons {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    margin-top: 20px;
  }
}
</style>