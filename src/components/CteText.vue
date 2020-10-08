<template>
  <div class="cte__container">
    <div
      v-if="!editing"
      class="cte__text"
      @click="startEditing"
    >
      {{ value }}
    </div>
    <input
      v-else
      ref="textbox"
      v-model="internalValue"
      class="cte__input"
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
    // TODO support "save" parameter
    stopEditing () {
      this.editing = false
      this.$emit('input', this.internalValue)
    }
  }
}
</script>

<style>
.cte__container {
  display: inline-block;
  font-size: 16px;
  font-family: Arial;
}

.cte__text {
  padding: 3px 4px;
  font-size: inherit;
  font-family: inherit;
}

.cte__input {
  font-size: inherit;
  font-family: inherit;
  width: 100%;
  box-sizing: border-box;
}
</style>
