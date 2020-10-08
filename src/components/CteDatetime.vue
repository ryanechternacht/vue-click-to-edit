<template>
  <div class="cte-datetime__container">
    <div
      v-if="!editing"
      class="cte-datetime__label"
      @click="startEditing"
    >
      {{ dateFormatted }}
    </div>
    <input
      v-else
      ref="textbox"
      v-model="internalValue"
      v-bind="$attrs"
      class="cte-datetime__input"
      type="datetime-local"
      @blur="stopEditing"
    >
  </div>
</template>

<script>
import { parseISO, format } from 'date-fns'

export default {
  name: 'CteDateTime',
  inheritAttrs: false,
  props: {
    value: {
      type: String,
      default: null
    },
    displayFormat: {
      type: String,
      default: 'MM/dd/yyyy, hh:mm aa'
    }
  },
  data () {
    return {
      editing: false,
      internalValue: this.value
    }
  },
  computed: {
    dateFormatted () {
      return format(parseISO(this.internalValue), this.displayFormat)
    }
  },
  watch: {
    value () {
      this.internalValue = this.value
    }
  },
  methods: {
    startEditing () {
      this.editing = true
      this.$nextTick(() => {
        this.$refs.textbox.focus()
      })
    },
    stopEditing () {
      this.editing = false
      this.$emit('input', this.internalValue)
      this.$emit('editingComplete', { newValue: this.internalValue })
    }
  }
}
</script>

<style>
.cte-datetime__container {
  display: inline-block;
  font-size: 16px;
  font-family: Times;
  width: 250px;
}

.cte-datetime__label {
  padding: 5px 4px;
  font-size: inherit;
  font-family: inherit;
  letter-spacing: .03em;
}

.cte-datetime__input {
  font-size: inherit;
  font-family: inherit;
  width: 100%;
  box-sizing: border-box;
}
</style>
