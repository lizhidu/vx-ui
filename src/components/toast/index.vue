<template>
  <div class="vx-toast">
    <div :class="['vx-toast-inner','vx-toast-' + this.align]">
      <div class="vx-toast-content">
        <template v-if="type != 'default'">
          <spinner v-if="type==='loading'" class="vx-toast-loading" v-bind="spinnerProps"/>
          <i v-else :class="['vx-toast-icon',`vx-toast-${type}`]"></i>
          <br />
        </template>
        <slot></slot>
      </div>
    </div>
  </div>
</template>

<script>
import Popup from '../popup'
import Spinner from '../spinner'

export default {
  componentName: 'Toast',
  components: {
    Popup,
    Spinner
  },
  props: {
    open: {
      type: Boolean,
      default: false
    },
    align: {
      type: String,
      default: 'top'
    },
    duration: {
      type: Number,
      default: 2000
    },
    type: {
      type: String,
      default: 'default'
    },
    destroy: {
      type: Boolean,
      default: false
    },
    spinnerProps: {
      type: Object,
      default () {
        return {
          color: '#999',
          primaryColor: '#fff',
          size: 0.72
        }
      }
    }
  },
  mounted () {
    this.openChange(this.open)
  },
  methods: {
    openChange (value) {
      if (value) {
        requestAnimationFrame(() => {
          this.$el.style.display = 'table'
        })
        this.duration && setTimeout(() => {
          requestAnimationFrame(() => {
            this.$el.style.display = 'none'
            this.$emit('update:open', false).$emit('close')
            if (this.destroy) {
              this.$destroy()
            }
          })
        }, this.duration)
      }
    }
  },
  destroyed () {
    requestAnimationFrame(() => {
      this.$el.parentNode.removeChild(this.$el)
    })
  },
  watch: {
    open (value) {
      this.openChange(value)
    }
  }
}
</script>
