<template>
  <div class="vx-checker-group" :disabled="disabled">
    <slot></slot>
  </div>
</template>

<script>
import { input } from 'utils/mixins'

export default {
  componentName: 'CheckerGroup',
  mixins: [input],
  props: {
    value: {
      type: [Array, String],
      default () {
        return []
      }
    },
    max: {
      type: Number,
      default: 0
    }
  },
  methods: {
    handleChange (e) {
      if (this.max === 1) {
        this.$emit('input', [e.target.value]).$emit('change', [e.target.value])
      } else {
        if (e.target.checked && this.max !== 0 && this.value.length === this.max) {
          e.target.checked = false
          this.$toast({content: `选择项不得超过${this.max}个`})
        } else {
          let value = Object.assign([], this.value)
          if (e.target.checked) {
            value.indexOf(e.target.value) === -1 && value.push(e.target.value)
          } else {
            value.splice(value.indexOf(e.target.value), 1)
          }
          this.$emit('input', value).$emit('change', value)
        }
      }
    }
  }
}
</script>
