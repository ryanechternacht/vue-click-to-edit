<template>
  <base-cte
    :value="internalValue"
    @editingComplete="editingComplete"
    @focusInput="focusInput"
  >
    <template #display-component>
      ********
    </template>

    <template #edit-component="{ blur }">
      <input
        ref="input"
        v-model="internalValue"
        class="cte-password__input"
        type="password"
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
  data () {
    return {
      internalValue: this.value
    }
  },
  methods: {
    editingComplete ({ committed }) {
      if (committed) {
        this.$emit('editingComplete', {})
      }
    },
    focusInput () {
      this.$refs.input.focus()
    }
  }
}
</script>

<style scoped>
.cte-password__input {
  font-size: inherit;
  font-family: inherit;
  width: 100%;
  box-sizing: border-box;
}

>>> .cte-base__label {
  padding: 3px 4px;
}
</style>
