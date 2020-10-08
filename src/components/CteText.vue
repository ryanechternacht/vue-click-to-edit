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
      :value="value"
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
      editing: false
    }
  },
  methods: {
    startEditing () {
      this.editing = true
      this.$refs.textbox.focus()
    },
    // TODO support "save" parameter
    stopEditing () {
      this.editing = false
    }
  }
}
</script>

<style>

</style>
