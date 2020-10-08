<template>
  <div class="cte-select__container">
    <div
      v-if="!editing"
      class="cte-select__label"
      @click="startEditing"
    >
      {{ value }}
    </div>
    <select
      v-else
      ref="select"
      v-model="internalValue"
      v-bind="$attrs"
      class="cte-select__select"
      @blur="stopEditing"
    >
      <slot />
    </select>
  </div>
</template>

<script>
export default {
  name: 'CteText',
  inheritAttrs: false,
  props: {
    value: {
      type: String,
      default: ''
    }
  },
  data () {
    return {
      editing: false,
      internalValue: this.value
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
        this.$refs.select.focus()
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
.cte-select__container {
  display: inline-block;
  font-size: 16px;
  font-family: Times;
}

.cte-select__label {
  padding: 3px 4px;
  font-size: inherit;
  font-family: inherit;
}

.cte-select__select {
  font-size: inherit;
  font-family: inherit;
  width: 100%;
  box-sizing: border-box;
}
</style>
