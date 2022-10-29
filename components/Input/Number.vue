<template>
  <div class="flex flex-col space-y-1 w-full">
    <input
      v-model="values"
      type="number"
      :placeholder="placeholder"
      class="form-base form-none"
      :class="{
        'form-success': validate.field.success,
        'form-error': validate.max.error || validate.min.error || error,
      }"
      @keypress="onlyNumber"
      @input="$emit('input', values)"
    />
    <div class="flex space-x-1">
      <span
        v-if="validate.max.error"
        class="text-red-600 text-xs font-semibold"
      >
        {{ validate.max.msg }}
      </span>
      <span
        v-if="validate.min.error"
        class="text-red-600 text-xs font-semibold"
      >
        {{ validate.min.msg }}
      </span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    required: {
      default: false,
      type: Boolean,
    },
    min: {
      default: 1,
      type: Number,
    },
    max: {
      default: 20,
      type: Number,
    },
    placeholder: {
      default: null,
      type: String,
    },
    error: {
      default: false,
      type: Boolean,
    },

    value: {
      default: null,
    },
  },
  data() {
    return {
      values: this.value,
      validate: {
        max: {
          error: false,
          msg: null,
        },
        min: {
          error: false,
          msg: null,
        },
        field: {
          success: false,
        },
      },
    }
  },
  watch: {
    value(val) {
      this.values = val
    },
    values(val) {
      this.minOptions(val)
      this.maxOptions(val)
      if (this.required) {
        if (val.length < this.min || val.length > this.max) {
          this.validate.field.success = false
        } else {
          this.validate.field.success = true
        }
      }
    },
  },
  methods: {
    onlyNumber($event) {
      const keyCode = $event.keyCode ? $event.keyCode : $event.which
      if ((keyCode < 48 || keyCode > 57) && keyCode !== 46) {
        $event.preventDefault()
      }
    },
    minOptions(val) {
      if (val.length < this.min) {
        this.validate.min.error = true
        this.validate.min.msg = `Panjang minimal karakter ${this.min}`
      } else {
        this.validate.min.error = false
        this.validate.min.msg = null
      }
    },
    maxOptions(val) {
      if (val.length > this.max) {
        this.validate.max.error = true
        this.validate.max.msg = `Panjang karakter melebihi ${this.max}`
      } else {
        this.validate.max.error = false
        this.validate.max.msg = null
      }
    },
  },
}
</script>

<style></style>
