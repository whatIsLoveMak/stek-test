<!-- eslint-disable prettier/prettier -->
<template>
  <button class="button" :class="className" >{{innerText}}</button>
</template>
<!-- eslint-disable prettier/prettier -->
<script>
export default {
  name: 'tButton',
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
    innerText: {
        type: [String, Number],
        default: '',
    },
  },
}
</script>
<style lang="scss" scoped>
button {
  border-radius: 10px;
  text-align: center;
  padding: 10px 0px;
  font-size: 12px;
  line-height: 15px;
  transition: all 0.4s ease;
  max-width: 200px;
  width: 100%;
  font-weight: 600;
}
.button.disabled {
  color: #B4B4B4;
  background: #EEEEEE;
  border: 1px solid transparent;
  pointer-events: none;
}
.button {
  color: #EEEEEE;
  background: white;
  border: 1px solid #7BAE73;
  background: #7BAE73;
}
.red {
  background: #b96565;
  color: white;
}
</style>
