<template>
  <div
    v-click-outside="clickedAway"
    class="cte-base__container"
  >
    <div
      v-if="!editing"
      class="cte-base__label"
      @click="startEditing"
    >
      <slot name="display-component">
        {{ value }}
      </slot>
    </div>
    <div
      v-else
      class="cte-base__input"
    >
      <slot name="edit-component" />
      <input
        type="text"
        style="width: 100px"
      >
      <button
        v-if="allowCancel"
        class="cte-base__cancel"
        @click="editingCanceled"
      />
    </div>
  </div>
</template>

<script>
import ClickOutside from 'vue-click-outside'

export default {
  directives: {
    ClickOutside
  },
  props: {
    value: {
      type: String,
      default: ''
    },
    allowCancel: {
      type: Boolean,
      default: false
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
    clickedAway () {
      if (!this.editing) {
        return
      }

      this.editing = false
      this.editingCompleted(true)
    },
    editingCanceled () {
      this.editing = false
      this.editingCompleted(false)
    },
    editingCompleted (committed) {
      this.$emit('editingCompleted', { committed })
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

.cte-base__label:hover {
  text-decoration: underline;
}

.cte-base__input {
  display: flex;
  align-items: center;
}

.cte-base__cancel {
  margin-left: 8px;
  color: red;
  padding: 3px 6px;
  box-sizing: border-box;
  border: 1px solid #bbb;
  border-radius: 4px;
}

.cte-base__cancel:hover {
  background-color: #ddd;
  cursor: pointer;
}

.cte-base__cancel::after {
  content: "\2718";
}
</style>
