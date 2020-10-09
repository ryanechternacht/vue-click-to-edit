<template>
  <div class="cte-text__container">
    <div
      v-if="!editing"
      class="cte-text__label"
      @click="startEditing"
    >
      {{ value }}
    </div>
    <slot
      v-else
      :blur="stopEditing"
      name="edit-component"
    />
  </div>
</template>

<script>
export default {
  name: 'BaseCte',
  props: {
    value: {
      type: String,
      default: ''
    }
  },
  data () {
    return {
      editing: false,
      internalValue: this.value,
      demo: 5
    }
  },
  methods: {
    startEditing () {
      this.editing = true
      this.$nextTick(() => {
        this.$emit('focusInput')
      })
    },
    stopEditing () {
      this.editing = false
      this.$emit('editingComplete', { committed: true })
    }
  }
}
</script>

<style>

</style>
