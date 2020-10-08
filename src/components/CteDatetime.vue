<template>
  <div class="cte-datetime__container">
    <div
      v-if="!editing"
      class="cte-datetime__label"
      @click="startEditing"
    >
      {{ value }}
    </div>
    <input
      v-else
      ref="textbox"
      v-model="internalValue"
      class="cte-datetime__input"
      type="datetime-local"
      @blur="stopEditing"
    >
  </div>
</template>

<script>
export default {
  name: 'CteDateTime',
  props: {
    value: {
      type: String,
      default: ''
    }
  },
  data () {
    return {
      editing: true,
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
.cte-datetime__container {
  display: inline-block;
  font-size: 16px;
  font-family: Arial;
  width: 250px;
}

.cte-datetime__label {
  padding: 8px 4px;
  font-size: inherit;
  font-family: inherit;
}

.cte-datetime__input {
  font-size: inherit;
  font-family: inherit;
  width: 100%;
  box-sizing: border-box;
}
</style>
