<template>
  <label class="vx-checker">
    <input
      :type="myType"
      :checked="myChecked"
      :name="name"
      :value="value"
      :disabled="myDisabled"
      @change="handleChange"
      />
    <button type="button" :disabled="myDisabled">
      <slot></slot>
    </button>
  </label>
</template>

<script>
import { input } from 'utils/mixins'

export default {
  componentName: 'Checker',
  mixins: [input],
  props: {
    value: {
      type: [String]
    }
  },
  computed: {
    myChecked () {
      if (this.$parent && this.$parent.$options && this.$parent.$options.componentName === 'CheckerGroup' && this.$parent.value && this.$parent.value.indexOf) {
        return this.$parent.value.indexOf(this.value) > -1
      } else {
        return this.checked
      }
    },
    myType () {
      if (this.$parent && this.$parent.$options && this.$parent.$options.componentName === 'CheckerGroup') {
        return this.$parent.max === 1 ? 'radio' : 'checkbox'
      } else {
        return this.type
      }
    },
    myDisabled () {
      let disabled = this.disabled
      if (this.$parent && this.$parent.$options && this.$parent.$options.componentName === 'CheckerGroup' && this.$parent.max > 1 && this.$parent.value.length >= this.$parent.max) {
        return this.$parent.value.indexOf(this.value) === -1
      }
      return disabled
    }
  },
  methods: {
    handleChange (e) {
      if (this.$parent && this.$parent.$options && this.$parent.$options.componentName === 'CheckerGroup') {
        this.$parent.handleChange(e)
      } else {
        this.$emit('update:checked', e.target.checked).$emit('change', e)
      }
    }
  }
}
</script>
