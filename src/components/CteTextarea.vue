<template>
  <div class="cte-textarea__container">
    <div
      v-if="!editing"
      class="cte-textarea__label"
      @click="startEditing"
    >
      {{ value }}
    </div>
    <textarea
      v-else
      ref="textbox"
      rows="6"
      v-model="internalValue"
      v-bind="$attrs"
      class="cte-textarea__input"
      @blur="stopEditing"
    />
  </div>
</template>

<script>
export default {
  name: 'CteTextarea',
  inheritAttrs: false,
  props: {
    value: {
      type: String,
      default: null
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
.cte-textarea__container {
  display: inline-block;
  font-size: 16px;
  font-family: Times;
  width: 250px;
}

.cte-textarea__label {
  padding: 5px 4px;
  font-size: inherit;
  font-family: inherit;
  letter-spacing: .03em;
}

.cte-textarea__input {
  font-size: inherit;
  font-family: inherit;
  width: 100%;
  box-sizing: border-box;
}
</style>
