<template>
  <div class="cte-text__container">
    <div
      v-if="!editing"
      class="cte-text__label"
      @click="startEditing"
    >
      {{ value }}
    </div>
    <input
      v-else
      ref="textbox"
      v-model="internalValue"
      v-bind="$attrs"
      class="cte-text__input"
      @blur="stopEditing"
    >
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
.cte-text__container {
  display: inline-block;
  font-size: 16px;
  font-family: Arial;
}

.cte-text__label {
  padding: 3px 4px;
  font-size: inherit;
  font-family: inherit;
}

.cte-text__input {
  font-size: inherit;
  font-family: inherit;
  width: 100%;
  box-sizing: border-box;
}
</style>
