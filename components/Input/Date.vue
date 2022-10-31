<template>
  <div class="w-full flex flex-col space-y-1">
    <input
      v-model="values"
      :type="type"
      class="form-base"
      :disabled="disabled"
      :placeholder="placeholder"
      :class="{
        'form-success': validate.success,
        'form-error': validate.error,
      }"
      @input="$emit('input', values)"
    />
    <span v-if="validate.error" class="text-red-600 font-semibold text-xs">
      {{ validate.msg }}
    </span>
  </div>
</template>

<script>
export default {
  props: {
    value: {
      default: null,
      type: String,
    },
    disabled: {
      default: false,
      type: Boolean,
    },
    required: {
      default: false,
      type: Boolean,
    },
    placeholder: {
      default: null,
      type: String,
    },
    error: {
      default: false,
      type: Boolean,
    },

    type: {
      default: 'date',
      type: String,
    },
  },
  data() {
    return {
      values: this.value,

      validate: {
        error: false,
        msg: null,
        success: false,
      },
    }
  },
  watch: {
    value(val) {
      this.values = val
    },
    values(val) {
      if (this.required) {
        if (val) {
          this.validate.error = false
          this.validate.success = true
          this.validate.msg = ''
        } else {
          this.validate.error = true
          this.validate.success = false
          this.validate.msg = 'Field harus diisi'
        }
      }
    },
  },
}
</script>

<style></style>
