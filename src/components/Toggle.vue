<script>
  import { computed } from 'vue'
  const booleanMap = {
    true: true,
    false: false
  }
  export default {
    props: {
      disabled: {
        type: Boolean,
        default: () => false
      },
      option: {
        type: String,
        default: ''
      },
      value: {
        type: [Boolean, String],
        default: () => null
      }
    },
    emits: ['onInput', 'update:value'],
    setup (props, { emit }) {
      const defaultValue = computed(() => typeof (props.value) === 'string'
        ? booleanMap[props.value]
        : props.value
      )
      return {
        defaultValue,
        onInput (value) {
          emit('onInput', value)
          emit('update:value', value)
        }
      }
    }
  }
</script>

<template>
  <div class="toggle">
    <label :class="{disabled}" for="toggle">
      <input
        id="toggle"
        type="checkbox"
        :value="option"
        :checked="defaultValue"
        @input="onInput(!defaultValue)"
        :disabled ="disabled"
        >
        <div class="custom"></div>
    </label>
  </div>
  </template>
  
  <style scoped lang="sass">
  .toggle
    label
      width: 100%
      display: flex
      align-items: center
      justify-content: space-between
      transition: .3s
    input
      display: none
    .custom
      position: relative
      width: 36px
      height: 18px
      background-color: #F3EFFF
      transition: .4s
      border-radius: 20px
      border: 2px solid #F3EFFF
      box-sizing: content-box
      cursor: pointer
      &::before
        position: absolute
        content: ""
        height: 18px
        width: 18px
        border-radius: 18px
        background-color: white
        transition: .4s
      fill: #A5A3A9 !important
    input:checked ~ .custom
      background-color: #5314FF
      border-color: #5314FF
    input:checked ~ .custom::before
      transform: translateX(18px)
    .disabled .custom
      cursor: not-allowed
  
  </style>
  