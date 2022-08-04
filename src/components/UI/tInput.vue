<!-- eslint-disable prettier/prettier -->

<template>
    <label for="">
      <input :class="className" :placeholder="placeholder" :type="type" :value="value" @input="input">
    </label>
</template>
<!-- eslint-disable prettier/prettier -->
<script>
export default {
  name: 'tInput',
  components: {},
  data() {
    return {}
  },
  props: {
    placeholder: {
        type: [String, Number],
        default: '',
    },
    className: {
        type: Object,
        default: ()=>{},
    },
    type: {
        type: String,
        default: 'text',
    },
    value: {
        type: [String, Number],
        default: '',
    },
    innerLabel: {
        type: [String, Number],
        default: '',
    },
    errorInner: {
         type: Array,
      default: () => [],
    },
  },
  methods: {
    input(event) {
      let value = event.target.value
      this.$emit('input', value)
    },
  },
}
</script>
<style lang="scss" scoped>
    label {
      display: flex;
      flex-direction: column;
      margin-bottom: 10px;
      & span {
        font-size: 10px;
        line-height: 13px;
        margin-bottom: 4px;
        color: #49485E;
        position: relative;
        max-width: max-content;
      }
      & span::after {
        content: '';
        position: absolute;
        top: 0;
        right: -6px;
        width: 4px;
        height: 4px;
        background: #FF8484;
        border-radius: 50%;

      }
    }
    input {
      padding: 10px 16px;
      background: #FFFEFB;
      box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
      border-radius: 4px;
      margin-bottom: 4px;
      border: 1px solid transparent;
      &::placeholder {
        font-size: 12px;
        line-height: 15px;
        color: #B4B4B4;
      }
    }
    .error-message {
      font-size: 8px;
      line-height: 10px;
      color: #FF8484;
    }
    .error {
      border: 1px solid #FF8484;
    }
</style>
