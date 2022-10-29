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
      default: 'text',
      type: String,
    },
  },
  data() {
    return {
      values: this.value,
      /* eslint-disable no-useless-escape */
      reg: /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,24}))$/,
      /* eslint-disable no-useless-escape */
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
          if (this.type === 'email') {
            if (this.reg.test(val)) {
              this.validate.error = false
              this.validate.success = true
              this.validate.msg = null
            } else {
              this.validate.error = true
              this.validate.success = false
              this.validate.msg = 'Masukkan format email dengan benar'
            }
          } else {
            this.validate.error = false
            this.validate.success = true
            this.validate.msg = null
          }
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
