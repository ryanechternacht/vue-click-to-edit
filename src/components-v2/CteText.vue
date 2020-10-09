<template>
  <base-cte
    :value="internalValue"
    @editingComplete="editingComplete"
    @focusInput="focusInput"
  >
    <template #edit-component="{ blur }">
      <input
        ref="input"
        v-model="internalValue"
        class="cte-text__input"
        v-bind="$attrs"
        @blur="blur"
      >
    </template>
  </base-cte>
</template>

<script>
import BaseCte from './BaseCte'

export default {
  components: {
    BaseCte
  },
  props: {
    value: {
      type: String,
      default: ''
    }
  },
  data () {
    return {
      internalValue: this.value
    }
  },
  methods: {
    editingComplete ({ committed }) {
      if (committed) {
        this.$emit('input', this.internalValue)
        this.$emit('editingComplete', { newValue: this.internalValue })
      }
    },
    focusInput () {
      this.$refs.input.focus()
    }
  }
}
</script>

<style>
.cte-text__input {
  font-size: inherit;
  font-family: inherit;
  width: 100%;
  box-sizing: border-box;
}
</style>
