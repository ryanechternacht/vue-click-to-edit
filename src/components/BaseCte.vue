<template>
  <div class="cte-base__container">
    <div
      v-if="!editing"
      class="cte-base__label"
      @click="startEditing"
    >
      <slot name="display-component">
        {{ value }}
      </slot>
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
      editing: false
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
.cte-base__container {
  display: inline-block;
  font-size: 16px;
  font-family: Times;
}

.cte-base__label {
  font-size: inherit;
  font-family: inherit;
}
</style>
