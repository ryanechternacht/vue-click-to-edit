<template>
  <base-cte
    :value="internalValue"
    @editingComplete="editingComplete"
    @focusInput="focusInput"
  >
    <template #edit-component="{ blur }">
      <select
        ref="input"
        v-model="internalValue"
        class="cte-select__select"
        v-bind="$attrs"
        @blur="blur"
      >
        <slot />
      </select>
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

<style scoped>
.cte-select__select {
  font-size: inherit;
  font-family: inherit;
  width: 100%;
  box-sizing: border-box;
}

>>> .cte-base__label {
  padding: 3px 4px;
}
</style>
