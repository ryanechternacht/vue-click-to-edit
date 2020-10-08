<template>
  <div>
    <span
      v-if="!editing"
      @click="startEditing"
    >
      {{ value }}
    </span>
    <input
      v-else
      ref="textbox"
      v-model="internalValue"
      @blur="stopEditing"
    >
  </div>
</template>

<script>
export default {
  name: 'CteText',
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
    // TODO support "save" parameter
    stopEditing () {
      this.editing = false
      this.$emit('input', this.internalValue)
    }
  }
}
</script>

<style>

</style>
